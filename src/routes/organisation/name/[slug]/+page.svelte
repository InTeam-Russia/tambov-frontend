<script lang="ts">
    import ChevronLeft from "lucide-svelte/icons/chevron-left"
    import { Button } from "$lib/components/ui/button"

    import NoInnSection from "$lib/modules/NoInnSection/NoInnSection.svelte"
    import OrgsList from "$lib/modules/OrgsList/OrgsList.svelte"

    import getOrganisations from "$api/get-orgs-by-name.ts"

    export let data;

    let orgs = getOrganisations(data.slug)
    console.log(orgs)
    let error = orgs === "error"
</script>

{#if error}
<NoInnSection />
{:else}
<section class="mt-16 max-w-screen-lg mx-auto">
    <h2 class="text-4xl mb-4">
        <Button href="/" variant="outline" size="icon">
            <ChevronLeft />
        </Button>
        Поиск по названию
    </h2>
    <OrgsList orgs={orgs} />
</section>
{/if}