<script lang="ts">
    import { onMount } from "svelte";
    
    import ProjectCard from "$lib/ProjectCard.svelte";
    import Navigation from "$lib/Navigation.svelte";


    let scrollY = 0;
    let sections = [
        {
            name: "Introduction",
            element: null
        },
        {
            name: "Projects",
            element: null
        },
        {
            name: "About",
            element: null
        }
    ];
    let selection;

    function handleScroll() {
        window.requestAnimationFrame(() => scrollY = window.scrollY);
        selection = [...sections].reverse().find(({ element }) => element.offsetTop <= window.scrollY + 25);
    }

    onMount(() => {
        selection = [...sections].reverse().find(({ element }) => element.offsetTop <= window.scrollY + 25);
    });
</script>

<svelte:head>
    <title>tropical's site</title>
</svelte:head>

<svelte:window on:scroll={handleScroll} />

<Navigation bind:sections bind:selection />

<main>
    <section id="introduction" bind:this={sections[0].element}>
        <h1 style:--scroll-y="{scrollY}px">
            {#each "tropical" as char, i}
                <div class="character-wrapper" style:bottom="calc(var(--scroll-y) * {(((Math.random() * 10) + 1) / 10)})">
                    <span style:--index={i.toString()}>
                        {char}
                    </span>
                </div>
            {/each}
        </h1>
    </section>
    <section id="projects" bind:this={sections[1].element}>
        <header>
            Projects
            <a role="button" href="https://github.com/tropix126/" target="_blank" rel="noreferrer noopener">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16" width="16" height="16">
                    <path fill="currentColor" fill-rule="evenodd" d="M8 0C3.58 0 0 3.58 0 8c0 3.54 2.29 6.53 5.47 7.59.4.07.55-.17.55-.38 0-.19-.01-.82-.01-1.49-2.01.37-2.53-.49-2.69-.94-.09-.23-.48-.94-.82-1.13-.28-.15-.68-.52-.01-.53.63-.01 1.08.58 1.23.82.72 1.21 1.87.87 2.33.66.07-.52.28-.87.51-1.07-1.78-.2-3.64-.89-3.64-3.95 0-.87.31-1.59.82-2.15-.08-.2-.36-1.02.08-2.12 0 0 .67-.21 2.2.82.64-.18 1.32-.27 2-.27.68 0 1.36.09 2 .27 1.53-1.04 2.2-.82 2.2-.82.44 1.1.16 1.92.08 2.12.51.56.82 1.27.82 2.15 0 3.07-1.87 3.75-3.65 3.95.29.25.54.73.54 1.48 0 1.07-.01 1.93-.01 2.2 0 .21.15.46.55.38A8.013 8.013 0 0016 8c0-4.42-3.58-8-8-8z" />
                </svg>
            </a>
        </header>
        <div class="projects-container">
            <ProjectCard title="Fluent Svelte" href="https://fluent-svelte.vercel.app/">
                Svelte component library for building user interfaces faithful to Microsoft's Fluent Design System.
            </ProjectCard>
            <ProjectCard title="files.community" href="https://files.community/">
                The starting page for everything related to Files, the modern Windows file explorer.
            </ProjectCard>
            <ProjectCard title="Slate" href="https://slate-theme.netlify.app/">
                An optimized, consistent, and functional theme for @discord based on GitHub's design language.
            </ProjectCard>
            <ProjectCard title="SvelteKit Package Template" href="https://github.com/tropix126/sveltekit-package-template">
                A barebones project that provides the essentials for writing highly-optimized, reusable packages in Svelte.
            </ProjectCard>
            <ProjectCard title="betterdiscord.app" href="https://betterdiscord.app/">
                Website frontend for BetterDiscord, a modern discord client modification tool.
            </ProjectCard>
            <ProjectCard title="BetterDiscord Installer" href="https://github.com/betterdiscord/installer/">
                A simple standalone program which automates the installation, removal and maintenance of BetterDiscord.
            </ProjectCard>
            <ProjectCard title="Svelte ARIA Dialog" href="https://github.com/tropix126/svelte-aria-dialog/">
                A tiny svelte component that provides a mostly unstyled, WAI-ARIA accessible modal dialog with a few simple options.
            </ProjectCard>
            <ProjectCard title="Svelte Codesandbox" href="https://github.com/tropix126/svelte-codesandbox">
                A powerful Svelte wrapper component around the CodeSandbox editor embed.
            </ProjectCard>
        </div>
    </section>
<!--     <section id="about" bind:this={sections[2].element}>
        <h1>Hey there.</h1>
        <p>Thanks for checking out my site! I'm a US-located hobbyist web developer and designer who specializes in open source stuff. If you're interested in any of my projects, a star would be greatly appreciated. You can find my socials below.</p>
    </section> -->
</main>

<style lang="scss">
    @keyframes fade {
        from {
            opacity: 0;
        }
        to {
            opacity: 1;
        }
    }

    @keyframes letter-up {
        from {
            transform: translateY(100%);
        }
    }

    @keyframes nav-in {
        from {
            transform: translateX(-100%);
        }
    }

    @keyframes main-in {
        from {
            margin: 0;
        }
    }
    
    @keyframes section-in {
        from {
            margin: 0;
            inline-size: 100%;
            min-block-size: 100vh;
        }
    }

    @keyframes scroll-gutter-in {
        from {
            transform: translateY(calc(var(--scroll-gutter-direction, 1) * 100%));
        }
    }

    @keyframes projects-header-in {
        from {
            top: 0;
        }
    }

    :global(html:not([data-hydrated])) {
        opacity: 0;
        animation: fade 500ms linear 500ms forwards;
    }

    :global(html[data-hydrated]) {
        --initial-delay: 750ms;
        :global(.navigation-sidebar) {
            animation: nav-in 250ms cubic-bezier(0, 0, 0, 1) backwards var(--initial-delay);
        }
        main {
            animation: fade var(--initial-delay) linear backwards calc(var(--initial-delay) / 2), main-in 250ms cubic-bezier(0, 0, 0, 1) backwards var(--initial-delay);
            &::before,
            &::after {
                animation: scroll-gutter-in 250ms cubic-bezier(0, 0, 0, 1) backwards var(--initial-delay);
            }
        }
        section {
            animation: section-in 250ms cubic-bezier(0, 0, 0, 1) backwards var(--initial-delay);
            &#projects > header {
                animation: projects-header-in 250ms cubic-bezier(0, 0, 0, 1) backwards var(--initial-delay);
            }
        }
        .character-wrapper span {
            animation: letter-up 250ms cubic-bezier(0, 0, 0, 1) calc(100ms * var(--index) + var(--initial-delay)) backwards;
        }
    }

    :global(.navigation-sidebar) {
        position: fixed;
        left: 0;
    }

    main {
        --waves-1: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='filter'%3E%3CfeTurbulence baseFrequency='0.0025 0.005' numOctaves='1' seed='2'%3E%3C/feTurbulence%3E%3CfeDiffuseLighting lighting-color='%231e235e' surfaceScale='100'%3E%3CfeDistantLight azimuth='2' elevation='20' style='elevation: 24;'%3E%3C/feDistantLight%3E%3C/feDiffuseLighting%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23filter)'%3E%3C/rect%3E%3C/svg%3E");
        --waves-2: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='filter'%3E%3CfeTurbulence baseFrequency='0.0025 0.005' numOctaves='1' seed='2'%3E%3C/feTurbulence%3E%3CfeDiffuseLighting lighting-color='%23ff194a' surfaceScale='100'%3E%3CfeDistantLight azimuth='2' elevation='20' style='elevation: 24;'%3E%3C/feDistantLight%3E%3C/feDiffuseLighting%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23filter)'%3E%3C/rect%3E%3C/svg%3E");
        display: grid;
        flex: 1 1 auto;
        margin-block: 24px;
        margin-inline-start: 48px;
        &::before,
        &::after {
            content: "";
            position: fixed;
            inline-size: 100%;
            block-size: 24px;
            inset-inline-start: 0;
            background-color: #121212;
            z-index: 1;
        }
        &::before {
            --scroll-gutter-direction: -1;
            inset-block-start: 0;
        }
        &::after {
            --scroll-gutter-direction: 1;
            inset-block-end: 0;
        }
    }

    section {
        position: relative;
        margin-inline: 24px;
        padding: 24px;
        text-align: center;
        inline-size: calc(100% - 48px);
        min-block-size: calc(100vh - 48px);
        &#introduction {
            overflow: hidden;
            block-size: calc(100vh - 24px);
            padding-top: 48px;
            margin-top: -24px;
            display: flex;
            align-items: center;
            justify-content: center;
            background: var(--waves-1) center/cover no-repeat fixed;
            h1 {
                filter: saturate(2);
                position: fixed;
                display: flex;
                align-items: center;
                margin: 0;
                line-height: 1;
                letter-spacing: 1vw;
                text-transform: uppercase;
                font-size: clamp(40px, 8vw, 240px);
                font-weight: 800;
                user-select: none;
            }
        }
        &#projects {
            display: flex;
            flex-direction: column;
            background-color: #e6e6e6;
            padding: 0;
            header {
                flex: 0 0 auto;
                display: flex;
                justify-content: space-between;
                align-items: center;
                align-self: flex-start;
                position: sticky;
                top: 24px;
                font-size: 12px;
                text-transform: uppercase;
                letter-spacing: 3px;
                text-align: left;
                block-size: 52px;
                inline-size: 100%;
                padding-inline: 24px 12px;
                background-color: #000;
                a {
                    outline: none;
                    display: flex;
                    padding: 12px;
                    color: #cecece;
                    transition: 150ms ease;
                    border-radius: 50%;
                    &:hover {
                        color: #fff;
                    }
                    &:focus {
                        box-shadow: inset 0 0 0 2px #fff;
                    }
                }
                svg {
                    flex: 0 0 auto;
                    inline-size: 16px;
                    block-size: auto;
                }
            }
        }
        &#about {
            text-align: left;
            padding: 8vh;
            position: relative;
            contain: layout;
            overflow: hidden;
            background-color: #1a1a1a;
            &::before {
                content: "";
                position: absolute;
                inset-inline-start: 50%;
                inset-block-start: 50%;
                transform: translate(-50%, -50%) rotate(30deg) scale(1.5);
                inline-size: 100vw;
                block-size: 100vw;
                background-color: #252525;
                z-index: -1;
                mask: url("data:image/svg+xml;charset=utf-8,%3Csvg xmlns='http://www.w3.org/2000/svg' width='100' height='100'%3E%3Ccircle cx='50' cy='50' r='10'/%3E%3C/svg%3E") center/18px;
            }
            h1 {
                font-size: clamp(40px, 14vh, 240px);
                font-weight: 800;
                margin: 0;
                color: var(--accent);
                text-transform: none;
                letter-spacing: normal;
            }
            p {
                color: #cecece;
                line-height: 2;
                max-width: 48ch;
                font-size: clamp(16px, 3.6vh, 48px);
            }
        }
    }

    .projects-container {
        flex: 1 1 auto;
        display: grid;
        grid-gap: 1px;
        grid-template-columns: 1fr 1fr;
        background-color: #cecece;
        @media screen and (max-width: 758px) {
            grid-template-columns: auto;
        }
    }

    .character-wrapper {
        position: relative;
        display: inline-block;
        overflow: hidden;
        margin-right: 2.5vw;
        span {
            position: relative;
            display: inline-block;
            will-change: top;
            background: var(--waves-2) center/cover no-repeat fixed;
            color: transparent;
            background-clip: text;
        }
    }
</style>
