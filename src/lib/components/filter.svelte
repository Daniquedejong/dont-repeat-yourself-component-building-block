<script>


import { onMount } from "svelte";

export let data;
// console.log(data)

let selectedCategoryId = null;

onMount(() => {
    const queryParams = new URLSearchParams(window.location.search);
    const filterParam = queryParams.get("filter");
    if (filterParam) {
        // De filterqueryparameter bevat de geselecteerde categorie-ID
        selectedCategoryId = filterParam;
    }
});

// Functie om methoden te filteren
function filterMethodsByCategory() {
    if (selectedCategoryId === null) {
        return data.methods; // Geen categorie geselecteerd, retourneer alle methoden
    } else {
        return data.methods.filter(method => 
            method.categories.some(category => category.id === selectedCategoryId)
        );
    }
}
    
</script>



<section class="categories-mobile">
    <label for="touch"><span id="menu-icon">Categorieën</span></label>
    <input type="checkbox" id="touch" />
    <ul class="slide">
      <li class="categorie-name">
        <a href="?selectedCategoryId=clbm28czo0kny0bw3tl71hnq4#touch">Onderzoeken en begrijpen</a>
      </li>
      <li class="categorie-name">
        <a href="?selectedCategoryId=clbm2bwei0ku90bw26jca93on#touch">Organiseren en plannen</a>
      </li>
      <li class="categorie-name">
        <a href="?selectedCategoryId=clbm2cfuj0kt40bw30fo6ow2j#touch">Leren over anderen</a>
      </li>
      <li class="categorie-name">
        <a href="?selectedCategoryId=clbm298dc0kpu0bw3weflzwvw#touch">Leren over jezelf</a>
      </li>
      <li class="categorie-name">
        <a href="?selectedCategoryId=clbm2c6zs0kst0aw18ja2oafj#touch">Communiceren en presenteren</a>
      </li>
      <li class="categorie-name">
        <a href="?selectedCategoryId=clbm2bnf20kqw0aw159269x9i#touch">Creatief denken</a>
      </li>
    </ul>
  </section>
  
  <section class="categories">
    <section class="categories-container">
      <ul class="categorie-names">
      <li class="categorie-name">
          <a href="?selectedCategoryId=clbm28czo0kny0bw3tl71hnq4#touch">Onderzoeken en begrijpen</a>
      </li>
      <li class="categorie-name">
        <a href="?selectedCategoryId=clbm2bwei0ku90bw26jca93on#touch">Organiseren en plannen</a>
      </li>
      <li class="categorie-name">
        <a href="?selectedCategoryId=clbm2cfuj0kt40bw30fo6ow2j#touch">Leren over anderen</a>
      </li>
      <li class="categorie-name">
        <a href="?selectedCategoryId=clbm298dc0kpu0bw3weflzwvw#touch">Leren over jezelf</a>
      </li>
      <li class="categorie-name">
        <a href="?selectedCategoryId=clbm2c6zs0kst0aw18ja2oafj#touch">Communiceren en presenteren</a>
      </li>
      <li class="categorie-name">
        <a href="?selectedCategoryId=clbm2bnf20kqw0aw159269x9i#touch">Creatief denken</a>
      </li>
      </ul>
    </section>
  </section>







  <main class="tekenmethodes-main">
    <article class="methods">
      {#if data.methods.length > 0}
        {#each data.methods as method, index}
          <section class="method-container" data-index={index}>
            <a href="/tekenmethodes/{method.slug}" class="link-detail-page">
              {#if method.template && method.template.url}
                <img
                  class={method.categories[0].title.replaceAll(" ", "-")}
                  src={method.template.url}
                  alt={"Voorbeeld van " + method.title}
                  loading="lazy"
                />
              {:else}
                <img
                  class={method.categories[0].title.replaceAll(" ", "-")}
                  src="/assets/placeholder.webp"
                  alt="Placeholder"
                  loading="lazy"
                />
              {/if}
              <section class="methods-titles">
                <h2>{method.title}</h2>
              </section>
            </a>
          </section>
        {/each}
      {/if}
    </article>
  </main>








  <style>


    /* CATEGORIEEE */


    .categories-mobile {
      display: none;
    }

    .categories {
      display: grid;
      grid: ". category ." 1fr / 1fr 4fr 1fr;
      margin-bottom: 50px;
    }

    .categories-container {
      grid-area: category;
    }

    li a {
      text-decoration: none;
      color: var(--vtDarkBlue);
      font-family: var(--vtPrimaryFont);
      font-size: 20px;
      padding-left: 40px;
    }

    .categorie-names li {
      display: flex;
      align-items: center;
      padding-bottom: 30px;
      list-style: none;
      flex: 0 0 calc(33.33% - 20px);
    }

    .categorie-names {
      display: flex;
      flex-wrap: wrap;
    }

    .categorie-names li:nth-child(1)::before {
      left: 10%;
      content: url(/assets/0-logo/1-icons/onderzoeken-en-begrijpen.svg);
    }

    .categorie-names li:nth-child(2)::before {
      right: 10%;
      content: url(/assets/0-logo/1-icons/organiseren-en-plannen.svg);
    }

    .categorie-names li:nth-child(3)::before {
      left: 10%;
      content: url(/assets/0-logo/1-icons/leren-over-anderen.svg);
    }

    .categorie-names li:nth-child(4)::before {
      left: 10%;
      content: url(/assets/0-logo/1-icons/leren-over-jezelf.svg);
    }

    .categorie-names li:nth-child(5)::before {
      left: 10%;
      content: url(/assets/0-logo/1-icons/communiceren.svg);
    }

    .categorie-names li:nth-child(6)::before {
      left: 10%;
      content: url(/assets/0-logo/1-icons/creatief.svg);
    }


  </style>