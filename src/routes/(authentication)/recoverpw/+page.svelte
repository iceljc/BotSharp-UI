<script>
	import Headtitle from '$lib/common/shared/HeadTitle.svelte';
	import { PUBLIC_LOGO_URL, PUBLIC_COMPANY_NAME } from '$env/static/public';
</script>

<Headtitle title="Recover Password" />

<div class="recover-hero relative flex min-h-screen items-center overflow-hidden dark:bg-gray-900">
	<!-- Decorative ambient background (matches login/register/home) -->
	<div class="recover-bg" aria-hidden="true">
		<span class="blob blob--primary"></span>
		<span class="blob blob--info"></span>
		<span class="blob blob--success"></span>
		<span class="grid-overlay"></span>
	</div>

	<div class="relative z-10 mx-auto w-full max-w-7xl px-4">
		<div class="flex min-h-screen items-center justify-center">
			<div class="w-full md:w-5/6 lg:w-2/3 xl:w-1/2">
				<div class="animate-slide-in-up py-8">

					<!-- Card -->
					<div class="recover-card overflow-hidden rounded-3xl bg-white/90 ring-1 ring-black/5 backdrop-blur-xl dark:bg-gray-800/90 dark:ring-white/10">

						<!-- Gradient header -->
						<div class="recover-header relative flex flex-col items-center justify-between gap-6 overflow-hidden bg-linear-to-br from-primary to-primary-hover px-6 py-8 text-center text-white md:flex-row md:gap-0 md:px-8 md:py-10 md:text-left">
							<span class="header-shine" aria-hidden="true"></span>
							<div class="relative z-10 flex-1">
								<div class="mb-6 flex justify-center md:justify-start">
									<a href="/">
										<div class="flex h-20 w-20 items-center justify-center rounded-full border-2 border-white/30 bg-white shadow-md transition-transform hover:scale-105">
											<img src={PUBLIC_LOGO_URL} alt="Logo" class="h-12 w-12 rounded-[20%] object-cover" />
										</div>
									</a>
								</div>
								<h2 class="mb-1 text-3xl font-bold drop-shadow-sm">Forgot password?</h2>
								<p class="text-lg opacity-90">No worries — we'll email you reset instructions</p>
							</div>
							<div class="relative z-10 md:ml-8 md:shrink-0">
								<img src="images/profile-img.png" alt="Reset password illustration" class="recover-illustration max-w-[120px] drop-shadow-lg md:max-w-[150px]" />
							</div>
						</div>

						<!-- Form body -->
						<div class="px-6 py-8 md:px-8 md:py-10">
							<!-- Info alert -->
							<div class="mb-6 flex items-center gap-2 rounded-xl bg-info/10 px-4 py-3 text-sm font-medium text-info" role="alert">
								<i class="mdi mdi-information-outline shrink-0 text-base leading-none" aria-hidden="true"></i>
								<span>Enter your email and we'll send instructions to reset your password.</span>
							</div>

							<form action="page/dashboard">
								<!-- Email -->
								<div class="mb-8">
									<label for="useremail" class="mb-2 block text-sm font-semibold text-gray-700 dark:text-gray-300">Email</label>
									<div class="relative">
										<i class="mdi mdi-email-outline pointer-events-none absolute left-4 top-1/2 z-10 -translate-y-1/2 text-xl text-gray-500 dark:text-gray-400" aria-hidden="true"></i>
										<input
											type="email"
											id="useremail"
											class="h-12 w-full rounded-xl border-2 border-gray-200 bg-white pl-[3.25rem] pr-4 text-base text-gray-900 transition-colors placeholder:text-gray-400 focus:border-primary focus:outline-none focus:ring-2 focus:ring-primary/15 disabled:opacity-70 dark:border-gray-600 dark:bg-gray-800 dark:text-white"
											placeholder="Enter your email"
										/>
									</div>
								</div>

								<!-- Submit -->
								<div class="mb-2 flex justify-center">
									<button
										type="submit"
										class="reset-btn h-14 min-w-[200px] rounded-xl px-8 text-lg font-semibold text-white transition-all hover:-translate-y-0.5 active:translate-y-0"
									>
										<i class="mdi mdi-email-send-outline mr-2"></i>
										Send instructions
									</button>
								</div>
							</form>
						</div>
					</div>

					<!-- Footer -->
					<div class="mt-8 text-center">
						<p class="mb-4 text-sm text-gray-600 dark:text-gray-300">
							Remember your password?
							<a href="login" class="ml-1 font-semibold text-primary transition-colors hover:text-primary-hover hover:underline">
								Sign in
							</a>
						</p>
						<p class="text-xs text-gray-500 dark:text-gray-400">
							© {new Date().getFullYear()} {PUBLIC_COMPANY_NAME}. Crafted with
							<i class="mdi mdi-heart text-danger"></i> by Open Source community
						</p>
					</div>

				</div>
			</div>
		</div>
	</div>
</div>

<style>
	/* ---- Ambient background (mirrors login/register/home) ---- */
	.recover-hero {
		background:
			radial-gradient(120% 120% at 50% 0%, #ffffff 0%, #f7f5fc 45%, #f1eefb 100%);
	}

	:global(.dark) .recover-hero {
		background:
			radial-gradient(120% 120% at 50% 0%, #1f2430 0%, #171a23 55%, #11131a 100%);
	}

	.recover-bg {
		position: absolute;
		inset: 0;
		z-index: 0;
		overflow: hidden;
		pointer-events: none;
	}

	.blob {
		position: absolute;
		border-radius: 9999px;
		filter: blur(80px);
		opacity: 0.4;
		will-change: transform;
	}

	.blob--primary {
		width: 36rem;
		height: 36rem;
		top: -12rem;
		left: -10rem;
		background: var(--color-primary);
		animation: drift-a 18s ease-in-out infinite;
	}

	.blob--info {
		width: 30rem;
		height: 30rem;
		top: -6rem;
		right: -8rem;
		background: var(--color-info);
		opacity: 0.3;
		animation: drift-b 22s ease-in-out infinite;
	}

	.blob--success {
		width: 26rem;
		height: 26rem;
		bottom: -10rem;
		left: 35%;
		background: var(--color-success);
		opacity: 0.24;
		animation: drift-a 26s ease-in-out infinite reverse;
	}

	.grid-overlay {
		position: absolute;
		inset: 0;
		background-image: radial-gradient(circle, rgba(111, 66, 193, 0.07) 1px, transparent 1px);
		background-size: 26px 26px;
		mask-image: radial-gradient(75% 60% at 50% 45%, #000 0%, transparent 75%);
		-webkit-mask-image: radial-gradient(75% 60% at 50% 45%, #000 0%, transparent 75%);
	}

	/* ---- Card ---- */
	.recover-card {
		box-shadow:
			0 30px 60px -20px rgba(52, 58, 64, 0.28),
			0 12px 24px -12px rgba(111, 66, 193, 0.25);
		transition: transform 0.35s ease, box-shadow 0.35s ease;
	}

	.recover-card:hover {
		transform: translateY(-3px);
		box-shadow:
			0 38px 72px -20px rgba(52, 58, 64, 0.32),
			0 16px 30px -12px rgba(111, 66, 193, 0.32);
	}

	/* ---- Header sheen + floating illustration ---- */
	.header-shine {
		position: absolute;
		inset: 0;
		z-index: 0;
		background:
			radial-gradient(120% 100% at 100% 0%, rgba(255, 255, 255, 0.28), transparent 55%),
			radial-gradient(80% 120% at 0% 100%, rgba(0, 0, 0, 0.12), transparent 60%);
	}

	.recover-illustration {
		animation: float 6s ease-in-out infinite;
	}

	/* ---- Submit button (matches login/register/home CTA glow) ---- */
	.reset-btn {
		background: linear-gradient(120deg, var(--color-primary), #8a5cd6);
		box-shadow:
			0 12px 26px -6px rgba(111, 66, 193, 0.55),
			inset 0 1px 0 rgba(255, 255, 255, 0.25);
	}

	.reset-btn:hover:not(:disabled) {
		filter: brightness(1.05);
		box-shadow:
			0 18px 34px -6px rgba(111, 66, 193, 0.65),
			inset 0 1px 0 rgba(255, 255, 255, 0.25);
	}

	/* ---- Keyframes ---- */
	@keyframes float {
		0%, 100% { transform: translateY(0); }
		50% { transform: translateY(-10px); }
	}

	@keyframes drift-a {
		0%, 100% { transform: translate(0, 0) scale(1); }
		50% { transform: translate(40px, 30px) scale(1.08); }
	}

	@keyframes drift-b {
		0%, 100% { transform: translate(0, 0) scale(1); }
		50% { transform: translate(-35px, 25px) scale(1.1); }
	}

	@media (prefers-reduced-motion: reduce) {
		.blob,
		.recover-illustration,
		.recover-card {
			animation: none !important;
		}
		.recover-card,
		.reset-btn {
			transition: none;
		}
	}
</style>

