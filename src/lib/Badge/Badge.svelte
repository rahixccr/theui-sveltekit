<script lang="ts">
  import type { ROUNDED } from "$lib/types"
  import { twMerge } from "tailwind-merge"
  import { getRounded } from "$lib/functions"

  export let text     : string  | undefined = undefined
  export let title    : string  | undefined = text
  export let grow     : boolean = false
  export let topFixed : boolean             = false
  export let round    : ROUNDED = "full"

  let getClasses = () => {
    let cls = "items-center justify-center whitespace-nowrap select-none bg-brand-primary-500 text-on-brand-primary-500 inline-block text-[1em] leading-[1em] font-medium p-[.35em] "
    cls += !grow ? "text-xs !leading-[.8em] " : ""
    cls += topFixed ? "absolute transform translate-x-1/2 rtl:-translate-x-1/2 -translate-y-1/2 top-0 end-0 border-4 border-primary" : ""
    cls += round !== "none" ? getRounded(round) : ""
    return cls
  }
</script>

<span class="theui-badge {twMerge(getClasses(), $$props?.class)}{getRounded(round)}">
  {text??""}
  <span class="sr-only">{title??"Badge"}</span>
</span>