<script lang="ts">

  import { Paginator } from '@skeletonlabs/skeleton';
  import { Accordion, AccordionItem } from '@skeletonlabs/skeleton';
  import { Autocomplete } from '@skeletonlabs/skeleton';
  import type { AutocompleteOption } from '@skeletonlabs/skeleton';
  import { goto } from '$app/navigation';

  // Sample data for the table dossier
  let rows = [
      { id: 1, refStelliant: 'TX20246942', date: '31/12/2024',assureur:'LA BANQUE POSTALE',typeSin:'Incendie',status:'A Qualifier' },
      { id: 2, refStelliant: 'TX20246942', date: '31/12/2024',assureur:'LA BANQUE POSTALE',typeSin:'Incendie',status:'A Qualifier' },
      { id: 3, refStelliant: 'TX20246942', date: '31/12/2024',assureur:'LA BANQUE POSTALE',typeSin:'Incendie',status:'A Qualifier' }
  ];

  function handleRowClick(id) {
      goto(`/dossier/${id}`);
  }

</script>

<div class="container h-full mx-auto justify-center">
  <div class="card mt-5 p-2">
    <Accordion>
      <AccordionItem>
        <svelte:fragment slot="lead">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="size-6">
            <path stroke-linecap="round" stroke-linejoin="round" d="m21 21-5.197-5.197m0 0A7.5 7.5 0 1 0 5.196 5.196a7.5 7.5 0 0 0 10.607 10.607Z" />
          </svg>
        </svelte:fragment>
        <svelte:fragment slot="summary">Recherche</svelte:fragment>
        <svelte:fragment slot="content">
          <form class="flex flex-col">
            <div class="flex flex-row gap-5">
            <label class="label">
              <span>Métier</span>
              <select class="select">
                <option value="1">DAB</option>
                <option value="2">CTR</option>
              </select>
            </label>
            <label class="label">
              <span>Assureur</span>
              <select class="select">
                <option value="1">MAIF</option>
                <option value="2">AXA</option>
              </select>
            </label>
            <label class="label">
              <span>Référence Stelliant</span>
              <input class="input" title="Input (text)" type="text" placeholder="ITER20241" />
            </label>
            <label class="label">
              <span>reception après le</span>
              <input class="input" title="Input (text)" type="date" />
            </label>
            <label class="label">
              <span>reception avant le</span>
              <input class="input" title="Input (text)" type="date" />
            </label>
            </div>
            <input class="btn variant-filled mt-5" type="button" value="Recherche" />
          </form>
        </svelte:fragment>
      </AccordionItem>
    </Accordion>  
  </div>
  <div class="table-container mt-5 p-2">
    <h2>Les dossiers</h2>
    <table class="table table-hover mt-2">
      <thead>
        <tr>
          <th>Référence Stelliant</th>
          <th>Date reception</th>
          <th>Assureur</th>
          <th>Type Sinistre</th>
          <th>Statut</th>
        </tr>
      </thead>
      <tbody>
        {#each rows as row}
          <tr on:click={() => handleRowClick(row.id)} style="cursor: pointer;">
            <td>{row.refStelliant}</td>
            <td>{row.date}</td>
            <td>{row.assureur}</td>
            <td>{row.typeSin}</td>
            <td><span class="badge variant-filled">{row.status}</span></td>
          </tr>
        {/each}
      </tbody>
      <tfoot>
        <tr>
          <th colspan="3">Nombre dossier</th>
          <td>{rows.length}</td>
        </tr>
      </tfoot>
    </table>
  </div>

</div>

<style lang="postcss">
</style>