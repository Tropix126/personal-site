<script>
    export let title = "unknown";
    export let href = "";
    export let github = "";
</script>

<a class="project-card" {href} target="_blank" rel="noreferrer noopener">
    <h3>{title}</h3>
    <p>
        <slot />
    </p>
    <div class="controls">
        {#if github}
            <div class="stars">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 32 32" aria-label="GitHub stars">
                    <path fill="currentColor" d="M16,6.52l2.76,5.58.46,1,1,.15,6.16.89L22,18.44l-.75.73.18,1,1.05,6.13-5.51-2.89L16,23l-.93.49L9.56,26.34l1-6.13.18-1L10,18.44,5.58,14.09l6.16-.89,1-.15.46-1L16,6.52M16,2l-4.55,9.22L1.28,12.69l7.36,7.18L6.9,30,16,25.22,25.1,30,23.36,19.87l7.36-7.17L20.55,11.22Z" />
                    <title>GitHub Stars</title>
                </svg>
                23
            </div>
        {/if}
        <span>View Project</span>
    </div>
</a>

<style lang="scss">
    .project-card {
        text-decoration: none;
        user-select: none;
        text-align: left;
        display: flex;
        flex-direction: column;
        height: auto;
        padding-block-end: 24px;
        padding: 24px;
        transition: 150ms ease;
        outline: none;
        background-color: #e6e6e6;
        &:hover {
            background-color: #f7f7f7;
        }
        &:focus {
            box-shadow: inset 0 0 0 2px var(--accent);
        }
        &:hover,
        &:focus {
            .controls span {
                text-decoration: underline;
                color: var(--accent);
            }
        }
        img {
            margin-block-end: 24px;
            object-fit: cover;
            width: 100%;
            height: auto;
        }
        h3 {
            margin: 0;
            font-size: 24px;
            letter-spacing: 2px;
            text-transform: uppercase;
            font-weight: 400;
            color: #2a2a2a;
        }
        p {
            margin: 0;
            margin-block-start: 24px;
            font-size: 16px;
            font-weight: 400;
            color: #626262;
        }
    }

    .controls {
        display: flex;
        align-items: center;
        justify-content: space-between;
        margin-top: auto;
        padding-top: 12px;
        span {
            margin-left: auto;
            font-size: 16px;
            font-weight: 400;
            color: var(--accent-alt);
            &::after {
                content: "->";
                letter-spacing: normal;
            }
        }
    }

    .stars {
        display: flex;
        align-items: center;
        line-height: normal;
        font-size: 14px;
        color: #626262;
        svg {
            flex: 0 0 auto;
            inline-size: 18px;
            block-size: auto;
            margin-inline-end: 6px;
            color: #2a2a2a;
        }
    }
</style>