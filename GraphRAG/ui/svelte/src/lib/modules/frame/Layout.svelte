<!--
  Copyright (C) 2024 Intel Corporation
  SPDX-License-Identifier: Apache-2.0
-->

<script lang="ts">
	import { onMount } from "svelte";
	import { page } from "$app/stores";
	import { browser } from "$app/environment";
	import { open } from "$lib/shared/stores/common/Store";
	import Scrollbar from "$lib/shared/components/scrollbar/Scrollbar.svelte";

	let root: HTMLElement
	onMount(() => {
		document.getElementsByTagName("body").item(0)!.removeAttribute("tabindex");
		// root.style.height = document.documentElement.clientHeight + 'px'
	});

	if (browser) {
		page.subscribe(() => {
			// close side navigation when route changes
			if (window.innerWidth > 768) {
				$open = true;
			}
		});
	}
</script>

<div bind:this={root} class='h-full overflow-hidden relative'>
	<div class="h-full flex items-start">
		<div class='relative flex flex-col h-full pl-0 w-full  bg-white'>
			<Scrollbar className="h-0 grow " classLayout="h-full" alwaysVisible={false}>
				<slot />
			</Scrollbar>
		</div>
	</div>
</div>
