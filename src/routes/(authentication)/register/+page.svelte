<script>
	import Headtitle from '$lib/common/shared/HeadTitle.svelte';
	import { goto } from '$app/navigation';
	import { PUBLIC_LOGO_URL, PUBLIC_COMPANY_NAME, PUBLIC_BRAND_NAME } from '$env/static/public';

	let username = $state('');
	let emailid = $state('');
	let password = $state('');
	let isOpen = $state(false);
	let msg = $state('');
	let status = $state('');

	/** @param {SubmitEvent} e */
	async function onSubmit(e) {
		e.preventDefault();
		try {
			if (username.trim() === '' || emailid.trim() === '' || password.trim() === '') {
				isOpen = true;
				msg = 'All Fields are required';
				status = 'danger';
				return false;
			}

			const response = await fetch('https://api-node.themesbrand.website/auth/signup', {
				method: 'POST',
				body: JSON.stringify({ email: emailid, password: password, username: username }),
				headers: {
					'Content-Type': 'application/json'
				}
			});

			const data = await response.json();

			if (response.ok && data.message === 'success') {
				sessionStorage.setItem('authUser', JSON.stringify(data));
				isOpen = true;
				msg = 'Registration success. Redirecting...';
				status = 'success';
				setTimeout(function () {
					goto('login');
				}, 1500);
			} else {
				isOpen = true;
				msg = 'error';
				status = 'danger';
				const error = data.data || 'An error occurred';
				msg = error;
				return error;
			}
		} catch (error) {
			console.error('Error:', error);
			return 'An error occurred';
		}
	}
</script>

<Headtitle title="Register" />

<div class="register-hero relative flex min-h-screen items-center overflow-hidden dark:bg-gray-900">
	<!-- Decorative ambient background (matches login/home) -->
	<div class="register-bg" aria-hidden="true">
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
					<div class="register-card overflow-hidden rounded-3xl bg-white/90 ring-1 ring-black/5 backdrop-blur-xl dark:bg-gray-800/90 dark:ring-white/10">

						<!-- Gradient header -->
						<div class="register-header relative flex flex-col items-center justify-between gap-6 overflow-hidden bg-linear-to-br from-primary to-primary-hover px-6 py-8 text-center text-white md:flex-row md:gap-0 md:px-8 md:py-10 md:text-left">
							<span class="header-shine" aria-hidden="true"></span>
							<div class="relative z-10 flex-1">
								<div class="mb-6 flex justify-center md:justify-start">
									<a href="/">
										<div class="flex h-20 w-20 items-center justify-center rounded-full border-2 border-white/30 bg-white shadow-md transition-transform hover:scale-105">
											<img src={PUBLIC_LOGO_URL} alt="Logo" class="h-12 w-12 rounded-[20%] object-cover" />
										</div>
									</a>
								</div>
								<h2 class="mb-1 text-3xl font-bold drop-shadow-sm">Create your account</h2>
								<p class="text-lg opacity-90">Join {PUBLIC_BRAND_NAME} and start building</p>
							</div>
							<div class="relative z-10 md:ml-8 md:shrink-0">
								<img src="images/profile-img.png" alt="Register illustration" class="register-illustration max-w-[120px] drop-shadow-lg md:max-w-[150px]" />
							</div>
						</div>

						<!-- Form body -->
						<div class="px-6 py-8 md:px-8 md:py-10">
							{#if isOpen}
								<div
									class="mb-6 rounded-xl px-4 py-3 font-medium {status === 'success' ? 'bg-green-100 text-green-800' : ''} {status === 'danger' ? 'bg-red-100 text-red-800' : ''}"
									role="alert"
								>
									{msg}
								</div>
							{/if}

							<form onsubmit={onSubmit}>
								<!-- Email -->
								<div class="mb-6">
									<label for="useremail" class="mb-2 block text-sm font-semibold text-gray-700 dark:text-gray-300">Email</label>
									<div class="relative">
										<i class="mdi mdi-email-outline pointer-events-none absolute left-4 top-1/2 z-10 -translate-y-1/2 text-xl text-gray-500 dark:text-gray-400" aria-hidden="true"></i>
										<input
											type="email"
											id="useremail"
											class="h-12 w-full rounded-xl border-2 border-gray-200 bg-white pl-[3.25rem] pr-4 text-base text-gray-900 transition-colors placeholder:text-gray-400 focus:border-primary focus:outline-none focus:ring-2 focus:ring-primary/15 dark:border-gray-600 dark:bg-gray-800 dark:text-white"
											placeholder="Enter your email"
											bind:value={emailid}
										/>
									</div>
								</div>

								<!-- Username -->
								<div class="mb-6">
									<label for="username" class="mb-2 block text-sm font-semibold text-gray-700 dark:text-gray-300">Username</label>
									<div class="relative">
										<i class="mdi mdi-account pointer-events-none absolute left-4 top-1/2 z-10 -translate-y-1/2 text-xl text-gray-500 dark:text-gray-400" aria-hidden="true"></i>
										<input
											type="text"
											id="username"
											class="h-12 w-full rounded-xl border-2 border-gray-200 bg-white pl-[3.25rem] pr-4 text-base text-gray-900 transition-colors placeholder:text-gray-400 focus:border-primary focus:outline-none focus:ring-2 focus:ring-primary/15 dark:border-gray-600 dark:bg-gray-800 dark:text-white"
											placeholder="Choose a username"
											bind:value={username}
										/>
									</div>
								</div>

								<!-- Password -->
								<div class="mb-8">
									<label for="userpassword" class="mb-2 block text-sm font-semibold text-gray-700 dark:text-gray-300">Password</label>
									<div class="relative">
										<i class="mdi mdi-lock-outline pointer-events-none absolute left-4 top-1/2 z-10 -translate-y-1/2 text-xl text-gray-500 dark:text-gray-400" aria-hidden="true"></i>
										<input
											type="password"
											id="userpassword"
											class="h-12 w-full rounded-xl border-2 border-gray-200 bg-white pl-[3.25rem] pr-4 text-base text-gray-900 transition-colors placeholder:text-gray-400 focus:border-primary focus:outline-none focus:ring-2 focus:ring-primary/15 dark:border-gray-600 dark:bg-gray-800 dark:text-white"
											placeholder="Create a password"
											bind:value={password}
										/>
									</div>
								</div>

								<!-- Submit -->
								<div class="mb-6 flex justify-center">
									<button
										type="submit"
										class="register-btn h-14 min-w-[200px] rounded-xl px-8 text-lg font-semibold text-white transition-all hover:-translate-y-0.5 active:translate-y-0"
									>
										<i class="mdi mdi-account-plus mr-2"></i>
										Register
									</button>
								</div>

								<!-- Divider -->
								<div class="relative my-8 text-center">
									<div class="absolute inset-x-0 top-1/2 h-px bg-gray-300 dark:bg-gray-600"></div>
									<span class="relative z-10 bg-white px-4 text-sm text-gray-500 dark:bg-gray-800 dark:text-gray-400">or sign up with</span>
								</div>

								<!-- Social -->
								<div class="mb-6 flex justify-center gap-4">
									<button
										type="button"
										class="flex h-[50px] w-[50px] items-center justify-center rounded-xl bg-[#3b5998] text-white transition-all hover:-translate-y-0.5 hover:bg-[#2d4373] hover:shadow-lg"
										aria-label="Sign up with Facebook"
									>
										<i class="mdi mdi-facebook text-2xl"></i>
									</button>
									<button
										type="button"
										class="flex h-[50px] w-[50px] items-center justify-center rounded-xl bg-[#1da1f2] text-white transition-all hover:-translate-y-0.5 hover:bg-[#0d8bd9] hover:shadow-lg"
										aria-label="Sign up with Twitter"
									>
										<i class="mdi mdi-twitter text-2xl"></i>
									</button>
									<button
										type="button"
										class="flex h-[50px] w-[50px] items-center justify-center rounded-xl bg-[#db4437] text-white transition-all hover:-translate-y-0.5 hover:bg-[#c23321] hover:shadow-lg"
										aria-label="Sign up with Google"
									>
										<i class="mdi mdi-google text-2xl"></i>
									</button>
								</div>

								<!-- Terms -->
								<p class="text-center text-sm text-gray-600 dark:text-gray-400">
									By registering you agree to the
									<button type="button" class="border-0 bg-transparent p-0 align-baseline font-medium text-primary transition-colors hover:text-primary-hover hover:underline">
										Terms of Use
									</button>
								</p>
							</form>
						</div>
					</div>

					<!-- Footer -->
					<div class="mt-8 text-center">
						<p class="mb-4 text-sm text-gray-600 dark:text-gray-300">
							Already have an account?
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
	/* ---- Ambient background (mirrors login/home) ---- */
	.register-hero {
		background:
			radial-gradient(120% 120% at 50% 0%, #ffffff 0%, #f7f5fc 45%, #f1eefb 100%);
	}

	:global(.dark) .register-hero {
		background:
			radial-gradient(120% 120% at 50% 0%, #1f2430 0%, #171a23 55%, #11131a 100%);
	}

	.register-bg {
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
	.register-card {
		box-shadow:
			0 30px 60px -20px rgba(52, 58, 64, 0.28),
			0 12px 24px -12px rgba(111, 66, 193, 0.25);
		transition: transform 0.35s ease, box-shadow 0.35s ease;
	}

	.register-card:hover {
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

	.register-illustration {
		animation: float 6s ease-in-out infinite;
	}

	/* ---- Submit button (matches login/home CTA glow) ---- */
	.register-btn {
		background: linear-gradient(120deg, var(--color-primary), #8a5cd6);
		box-shadow:
			0 12px 26px -6px rgba(111, 66, 193, 0.55),
			inset 0 1px 0 rgba(255, 255, 255, 0.25);
	}

	.register-btn:hover:not(:disabled) {
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
		.register-illustration,
		.register-card {
			animation: none !important;
		}
		.register-card,
		.register-btn {
			transition: none;
		}
	}
</style>

