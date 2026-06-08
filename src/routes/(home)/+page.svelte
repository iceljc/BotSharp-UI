<script>
    import { fade, fly } from 'svelte/transition';
    import { quintOut } from 'svelte/easing';
    import HeadTitle from "$lib/common/shared/HeadTitle.svelte";
    import {
        PUBLIC_LOGO_URL,
        PUBLIC_BRAND_NAME,
        PUBLIC_COMPANY_WEBSITE,
        PUBLIC_HOME_SLOGAN,
        PUBLIC_HOME_IMAGE
    } from '$env/static/public';
    import { onMount } from 'svelte';

    let mounted = $state(false);

    onMount(() => {
        mounted = true;
    });
</script>

<HeadTitle title="{PUBLIC_BRAND_NAME} Workspace" />

<div class="home-hero relative flex min-h-screen flex-col overflow-hidden px-4">
    <!-- Decorative ambient background -->
    <div class="home-bg" aria-hidden="true">
        <span class="blob blob--primary"></span>
        <span class="blob blob--info"></span>
        <span class="blob blob--success"></span>
        <span class="grid-overlay"></span>
    </div>

    <!-- Logo: absolute so it never shifts the centered hero below -->
    <div class="absolute top-6 right-6 z-20 sm:top-8 sm:right-8">
        <a
            href={PUBLIC_COMPANY_WEBSITE}
            class="inline-flex items-center rounded-2xl bg-white/60 p-2 shadow-sm ring-1 ring-black/5 backdrop-blur-md transition-all duration-300 hover:-translate-y-0.5 hover:shadow-md"
        >
            <img src={PUBLIC_LOGO_URL} alt="logo" class="h-9 w-auto sm:h-11" />
        </a>
    </div>

    <!-- Hero: vertically and horizontally centered on the viewport -->
    <div class="relative z-10 flex min-h-screen flex-col items-center justify-center text-center">
        {#if mounted}
            <div class="hero-image-wrap" transition:fade={{ delay: 200, duration: 600 }}>
                <span class="hero-glow" aria-hidden="true"></span>
                <img
                    src={PUBLIC_HOME_IMAGE}
                    alt=""
                    class="hero-image mx-auto w-full max-w-[260px] sm:max-w-sm md:max-w-md lg:max-w-lg"
                />
            </div>

            <div transition:fly={{ y: 24, delay: 450, duration: 700, easing: quintOut }}>
                <span
                    class="mt-4 inline-flex items-center gap-2 rounded-full bg-primary/10 px-4 py-1.5 text-xs font-medium tracking-wide text-primary uppercase ring-1 ring-primary/15"
                >
                    <span class="relative flex h-2 w-2">
                        <span class="absolute inline-flex h-full w-full animate-ping rounded-full bg-primary opacity-60"></span>
                        <span class="relative inline-flex h-2 w-2 rounded-full bg-primary"></span>
                    </span>
                    AI Agent Workspace
                </span>

                <h1 class="hero-title text-dark">
                    Welcome to
                    <span class="hero-brand">{PUBLIC_BRAND_NAME}</span>
                </h1>

                <p class="mx-auto mt-4 max-w-2xl text-base leading-relaxed text-pretty text-muted sm:text-lg">
                    {PUBLIC_HOME_SLOGAN}
                </p>

                <div class="mt-9 flex items-center justify-center">
                    <a href="login" class="cta-button group">
                        <span>Let&#39;s get started</span>
                        <svg
                            class="h-4 w-4 transition-transform duration-300 group-hover:translate-x-1"
                            viewBox="0 0 20 20"
                            fill="none"
                            stroke="currentColor"
                            stroke-width="2"
                            stroke-linecap="round"
                            stroke-linejoin="round"
                            aria-hidden="true"
                        >
                            <path d="M4 10h12M11 5l5 5-5 5" />
                        </svg>
                    </a>
                </div>
            </div>
        {/if}
    </div>
</div>

<style>
    .home-hero {
        background:
            radial-gradient(120% 120% at 50% 0%, #ffffff 0%, #f7f5fc 45%, #f1eefb 100%);
    }

    /* ---- Ambient background blobs ---- */
    .home-bg {
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
        opacity: 0.45;
        will-change: transform;
    }

    .blob--primary {
        width: 38rem;
        height: 38rem;
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
        opacity: 0.35;
        animation: drift-b 22s ease-in-out infinite;
    }

    .blob--success {
        width: 26rem;
        height: 26rem;
        bottom: -10rem;
        left: 30%;
        background: var(--color-success);
        opacity: 0.28;
        animation: drift-a 26s ease-in-out infinite reverse;
    }

    /* Subtle dotted grid for depth */
    .grid-overlay {
        position: absolute;
        inset: 0;
        background-image: radial-gradient(circle, rgba(111, 66, 193, 0.08) 1px, transparent 1px);
        background-size: 26px 26px;
        mask-image: radial-gradient(80% 60% at 50% 40%, #000 0%, transparent 75%);
        -webkit-mask-image: radial-gradient(80% 60% at 50% 40%, #000 0%, transparent 75%);
    }

    /* ---- Hero illustration ---- */
    .hero-image-wrap {
        position: relative;
        display: inline-block;
    }

    .hero-glow {
        position: absolute;
        inset: 8% 6%;
        z-index: -1;
        border-radius: 9999px;
        background: radial-gradient(closest-side, rgba(111, 66, 193, 0.22), transparent 70%);
        filter: blur(10px);
    }

    .hero-image {
        animation: float 6s ease-in-out infinite;
        filter: drop-shadow(0 24px 40px rgba(52, 58, 64, 0.18));
    }

    /* ---- Headline ---- */
    .hero-title {
        display: block;
        font-weight: 600;
        font-size: 1.25rem;   /* text-4xl */
        line-height: 1.15;
        padding: 20px 0px 10px 0px;
    }

    /* ---- Brand gradient text ---- */
    .hero-brand {
        background: linear-gradient(
            100deg,
            var(--color-primary) 0%,
            var(--color-info) 55%,
            var(--color-primary) 100%
        );
        background-size: 200% auto;
        -webkit-background-clip: text;
        background-clip: text;
        color: transparent;
        animation: shine 6s linear infinite;
    }

    /* ---- CTA ---- */
    .cta-button {
        display: inline-flex;
        align-items: center;
        gap: 0.6rem;
        padding: 0.85rem 1.9rem;
        font-size: 0.95rem;
        font-weight: 500;
        color: #fff;
        border-radius: 9999px;
        background: linear-gradient(120deg, var(--color-primary), #8a5cd6);
        box-shadow:
            0 10px 24px -6px rgba(111, 66, 193, 0.55),
            inset 0 1px 0 rgba(255, 255, 255, 0.25);
        transition: transform 0.25s ease, box-shadow 0.25s ease, filter 0.25s ease;
    }

    .cta-button:hover {
        transform: translateY(-2px);
        filter: brightness(1.05);
        box-shadow:
            0 16px 32px -6px rgba(111, 66, 193, 0.65),
            inset 0 1px 0 rgba(255, 255, 255, 0.25);
    }

    .cta-button:focus-visible {
        outline: 2px solid var(--color-primary);
        outline-offset: 3px;
    }

    /* ---- Keyframes ---- */
    @keyframes float {
        0%, 100% { transform: translateY(0); }
        50% { transform: translateY(-14px); }
    }

    @keyframes shine {
        to { background-position: 200% center; }
    }

    @keyframes drift-a {
        0%, 100% { transform: translate(0, 0) scale(1); }
        50% { transform: translate(40px, 30px) scale(1.08); }
    }

    @keyframes drift-b {
        0%, 100% { transform: translate(0, 0) scale(1); }
        50% { transform: translate(-35px, 25px) scale(1.1); }
    }

    /* Respect users who prefer reduced motion */
    @media (prefers-reduced-motion: reduce) {
        .hero-image,
        .hero-brand,
        .blob,
        .cta-button {
            animation: none !important;
        }
        .cta-button {
            transition: none;
        }
    }
</style>
