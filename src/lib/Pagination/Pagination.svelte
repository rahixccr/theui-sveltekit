<script lang="ts">
    import type { BUTTON_SIZE } from "$lib/types"
    import { createEventDispatcher } from "svelte"
    import { twMerge } from "tailwind-merge"
    import { Button, ButtonGroup } from "$lib"

    export let prevBtn: string = "&larr; Prev"
    export let nextBtn: string = "Next &rarr;"
    export let size: BUTTON_SIZE = "md"
    export let buttonStyle: string = ""
    export let minimalMode: boolean = false
    export let activeButtonStyle: string = ""
    export let align: 'start' | 'center' | 'end' = "center"
    export let variant: 'bordered' | 'flat' = "bordered"

    export let data: Array<{url: string, active?: boolean}> = []

    const dispatch  = createEventDispatcher()
    const previous  = () => dispatch("previous")
    const next      = () => dispatch("next")

    let getNumLinkClass = (active: boolean|undefined = undefined) => active ?
                          twMerge("bg-brand-primary-500 text-on-brand-primary-500", activeButtonStyle) :
                          twMerge("bg-transparent text-default hover:bg-brand-primary-500", buttonStyle)
</script>

<!-- {#if data.length > 0 || ((!data || data?.length < 1) && minimalMode)} -->
{#if minimalMode || data.length > 0}
    <div class="theui-pagination flex" class:justify-center={align=="center"} class:justify-end={align=="end"}>
        <ButtonGroup label="Pagination" {size} round="none" class={twMerge("", $$props?.class)} {variant} outline={true}>
            <Button class={getNumLinkClass()} on:click={previous} label={prevBtn} ariaLabel="Pagination link: previous"/>
            {#if !minimalMode}
                {#each data as link, i}
                <Button href={link.url} class={getNumLinkClass(link?.active)} label={(i+1).toString()} ariaLabel="Pagination page {i+1}"/>
                {/each}
            {/if}
            <Button class={getNumLinkClass()} on:click={next} label={nextBtn} ariaLabel="Pagination link: next"/>
        </ButtonGroup>
    </div>
{/if}
