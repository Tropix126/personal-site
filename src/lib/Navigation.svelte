<script lang="ts">
    interface Section {
        element: HTMLElement;
        name: string;
    }

    export let sections: Section[];
    export let selection: Section;
</script>

<aside class="navigation-sidebar">
    <nav>
        {#each sections as { name, element }}
            <a class:active={selection?.element === element} href={`#${name.toLowerCase().replace(/ /g, "-")}`}>
                {name}
            </a>
        {/each}
    </nav>
</aside>

<style lang="scss">
    .navigation-sidebar {
        z-index: 2;
        display: flex;
        flex-direction: column;
        align-items: center;
        inset-inline-start: 0;
        inset-block-start: 0;
        padding-block: 6px;
        position: fixed;
        inline-size: 48px;
        block-size: 100vh;
        background-color: #1a1a1a;
        nav {
            display: flex;
            transform: rotate(90deg) translateX(50%);
        }
        a {
            position: relative;
            margin-right: 12px;
            color: #9f9f9f;
            transition: 150ms ease;
            text-transform: uppercase;
            font-weight: 700;
            letter-spacing: 2px;
            font-size: 12px;
            text-decoration: none;
            &::after {
                content: "";
                display: block;
                position: absolute;
                inset-block-end: -4px;
                inset-inline-start: 0;
                inline-size: 100%;
                block-size: 2px;
                background-color: var(--accent);
                transition: 150ms cubic-bezier(0, 0.6, 0.2, 1);
                transform: scaleX(0);
                transform-origin: left;
            }
            &:hover {
                color: #cecece;
            }
            &:active {
                color: #909090;
            }
            &.active {
                color: #fff;
                &:active {
                    color: #cecece;
                }
                &::after {
                    transform: scaleX(1);
                }
            }
        }
    }
</style>