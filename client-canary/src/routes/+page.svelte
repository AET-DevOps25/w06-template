<script lang="ts">
    import { onMount } from "svelte";
    import "../app.css";
    import Icon from "@iconify/svelte";
    import { env } from '$env/dynamic/public';

    import FoodCard from './FoodCard.svelte';
    import type { Meal } from '$lib/types';
    import type { PageProps } from "./$types";

    let { data }: PageProps = $props();

    // For more information on runes and reactivity, see: https://svelte.dev/docs/svelte/what-are-runes
    let meals: Meal[] = data.meals;

    // Note: The data loading is now done in the +page.ts file (compared to the W03 exercise)
    // and passed to this component as props. This is a more efficient way to load data in SvelteKit.
</script>

<!-- Canary Deployment Banner -->
<div class="bg-yellow-300 text-black p-4 text-center font-bold text-lg">
    🚀 THIS IS THE NEW VERSION (CANARY DEPLOYMENT)
</div>

<main>
    <header>
        <h1>Garching Campus Canteen (v2, completely different!) </h1>
        <p>Today's menu offerings</p>
    </header>

    {#if meals.length === 0}
        <div class="no-results">
            <p>Loading menu items...</p>
        </div>
    {:else}
        <div class="food-grid">
            {#each meals as meal}
                <FoodCard {meal}/>
            {/each}
        </div>
    {/if}

    {#if meals.length === 0 && meals.length > 0}
        <div class="no-results">
            No menu items match your filters. Try changing your selection.
        </div>
    {/if}
</main>
