<script>
	import { onMount } from 'svelte';

	// ใช้ $state() ครอบค่าเริ่มต้น เพื่อให้ UI อัปเดตเมื่อค่าเปลี่ยน (Svelte 5)
	let step = $state(0);
	let progress = $state(0);

	let igUsername = $state('');
	let loginError = $state(false);

	let envelopeOpen = $state(false);
	let cardPulled = $state(false);

	// ชื่อเจ้าของวันเกิด (เป็น const ค่าไม่เปลี่ยน ไม่ต้องใส่ $state)
	const targetIG = 'panchw_';
	const name = 'Panchw';

	// [Step 0] อนิเมชันจำลองการโหลด 0-100%
	onMount(() => {
		const interval = setInterval(() => {
			progress += Math.floor(Math.random() * 5) + 1; // สุ่มเพิ่มทีละนิดให้ดูเหมือนโหลดจริง
			if (progress >= 100) {
				progress = 100;
				clearInterval(interval);
				setTimeout(() => {
					step = 1; // เปลี่ยนไปหน้า Login
				}, 800);
			}
		}, 100);
	});

	// [Step 1] ฟังก์ชันเช็คชื่อ IG
	function handleLogin() {
		if (igUsername.trim().toLowerCase() === targetIG) {
			loginError = false;
			step = 2; // เปลี่ยนไปหน้ากำลังเขียนข้อความ

			// หน่วงเวลาหน้า "กำลังเขียนข้อความ" 3 วินาที
			setTimeout(() => {
				step = 3; // เปลี่ยนไปหน้าซองจดหมาย
			}, 3000);
		} else {
			loginError = true;
		}
	}

	// รองรับการกดปุ่ม Enter เพื่อ Login
	/** @param {KeyboardEvent} e */
	function handleKeyPress(e) {
		if (e.key === 'Enter') handleLogin();
	}

	// [Step 3] ฟังก์ชันเปิดซองจดหมาย
	function openEnvelope() {
		if (!envelopeOpen) {
			envelopeOpen = true;
			// รอให้ฝาซองเปิดเสร็จ (0.6s) แล้วค่อยดึงการ์ดขึ้นมา
			setTimeout(() => {
				cardPulled = true;
			}, 600);
		}
	}
</script>

<main>
	{#if step === 0}
		<!-- ==================== หน้า 0: Loading 3D Cat ==================== -->
		<div class="screen-container">
			<h2 class="loading-text">กำลังโหลดความน่ารัก... {progress}%</h2>
			<div class="progress-container">
				<div class="progress-bar" style="width: {progress}%"></div>

				<!-- ลูกเล่น CSS 3D Cat Cube วิ่งไปตามแถบโหลด -->
				<div class="scene" style="left: {progress}%">
					<div class="cube">
						<div class="face front">🐱</div>
						<div class="face back">🐱</div>
						<div class="face right">🐾</div>
						<div class="face left">🐾</div>
						<div class="face top">🧡</div>
						<div class="face bottom">🧡</div>
					</div>
				</div>
			</div>
		</div>
	{:else if step === 1}
		<!-- ==================== หน้า 1: Login (กรอก IG) ==================== -->
		<div class="screen-container">
			<div class="card-glass">
				<div class="avatar-bounce">🐈</div>
				<h2 class="login-title">ยืนยันตัวตนคนน่ารัก 🧡</h2>
				<p>กรุณากรอก Instagram ของเจ้าของวันเกิด:</p>

				<input
					type="text"
					bind:value={igUsername}
					onkeypress={handleKeyPress}
					placeholder="เช่น panchw_"
				/>

				{#if loginError}
					<p class="error shake">
						เอ๊ะ ไม่ใช่นี่นา! พี่ของสวยของน้องมดไม่ได้ชื่อนี้นะ ลองพิมพ์ใหม่สิ
					</p>
				{/if}

				<button class="btn" onclick={handleLogin}>Enter</button>
			</div>
		</div>
	{:else if step === 2}
		<!-- ==================== หน้า 2: Transition ==================== -->
		<div class="screen-container">
			<div class="card-glass transition-glass">
				<div class="pencil-animation">✏️</div>
				<h2>น้องมดสุดเท่กำลังเขียนข้อความอวยพรวันเกิดให้พี่ปานคนสวย...</h2>
				<p>รอแป๊บนึงนะ ตั้งใจเขียนสุดๆ เลย 🧡</p>
			</div>
		</div>
	{:else if step === 3}
		<!-- ==================== หน้า 3: ซองจดหมายและหน้าการ์ด ==================== -->
		<div class="screen-container envelope-screen">
			{#if !envelopeOpen}
				<p class="instruction bounce">แตะที่ซองจดหมายเพื่อเปิด 💌</p>
			{/if}

			<button
				type="button"
				class="envelope-wrapper"
				onclick={openEnvelope}
				class:open={envelopeOpen}
				aria-pressed={envelopeOpen}
			>
				<!-- พื้นหลังซอง -->
				<div class="envelope-back"></div>

				<!-- ตัวการ์ดข้อความ -->
				<div class="letter" class:pulled={cardPulled}>
					<h1>Happy Birthday! 🎂</h1>
					<h2>To my dearest, {name} 🧡</h2>
					<div class="cat-wrapper">
						<span class="cat-placeholder">🐈</span>
					</div>
					<p class="message">
						ขอให้เธอมีความสุขมากๆนะ ขอให้โลกนี้น่ารักกับเธอ<br />
						เหมือนที่เธอน่ารักเสมอมาเลยนะ!<br />
						ต่อจากปีนี้เราจะไม่เเยกจากกันแล้วนะ<br />
						เค้าจะอยู่ด้วยกันกับเธอตลอดไปเลย 💕<br />
					</p>
					<p class="signature">
						คนที่รักเธอที่สุด<br />
					</p>
					<i class="signature_2"> BY ADIPA CHOUPOLSAT </i>
				</div>

				<!-- ฝาปิดซองด้านบน -->
				<div class="envelope-flap" class:open={envelopeOpen} aria-hidden={!envelopeOpen}></div>

				<!-- กระเป๋าซองจดหมายด้านหน้า -->
				<div class="envelope-pocket"></div>
			</button>
		</div>
	{/if}
</main>
