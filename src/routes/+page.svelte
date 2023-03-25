<script>
  import { fishQuery } from './store.js';
  import { fishProfile } from './store.js'; 
  import { onMount } from 'svelte';

  let finalFishArr;
  fishQuery.subscribe(value => {
		finalFishArr = value;
	});

  let finalFishProfile;
  fishProfile.subscribe(value => {
    finalFishProfile = value;
  });

  /** @type {import('./$types').PageData} */
  export let data;
  console.log(data)

let selected = "crimson-jobfish"
let mainFish = ""
function loadFish () {
  const name = `/profiles/${selected}`
  const fish = finalFishArr.filter(item => {
    if (item.Path == name) {
      console.log(item.Path)
      console.log("selected", selected)
      mainFish = item
      return item
    }
  })
  console.log(fish)
}

  onMount(()=> {loadFish()});
</script>

<main>
  <header>
    <nav>
      <h1 class="site-name">Fish Market API</h1>
      <form>
        <select bind:value={selected} on:change="{loadFish}">
          {#each finalFishProfile as fish2}
            <option value={fish2}>
              {fish2}
            </option>
          {/each}
        </select>
        </form>
    </nav>
    <div class="hero">
      <div class="title">
        <h2 class="fishName">
          {#if mainFish}
          {mainFish['Species Name']}
          {/if}
        </h2>
      </div>
      
    </div>
  </header>
  <section>
    <div class="container">
      <div class="left-area">
        {#if mainFish['Color']}
        <p><strong>Color</strong>: {@html mainFish['Color']}</p>
        {/if}
        
        {#if mainFish['Taste']}
        <p><strong>Taste</strong>: {@html mainFish['Taste']}</p>
        {/if}
        
        {#if mainFish['Texture']}
        <p><strong>Texture</strong>: {@html mainFish['Texture']}</p>
        {/if}
        
        {#if mainFish['Quote']}
        <p><strong>Quote</strong>: {@html mainFish['Quote']}</p>
        {/if}
        
        {#if mainFish['Health Benefits']}
        <p><strong>Health Benefits</strong>: {@html mainFish['Health Benefits']}</p>
        {/if}
        
        {#if mainFish['Location']}
        <p><strong>Location</strong>: {@html mainFish['Location']}</p>
        {/if}
        
        {#if mainFish['Physical Description']}
        <p><strong>Physical Description</strong>: {@html mainFish['Physical Description']}</p>
        {/if}
        
        {#if mainFish['Source']}
        <p><strong>Source</strong>: {@html mainFish['Source']}</p>
        {/if}

      </div>
      <div class="right-area">
  
      </div>
      <div class="photo-group"> 
        {#if mainFish['Image Gallery'] && mainFish['Image Gallery'].src}
        <img class="photo-img" src="{mainFish['Image Gallery'].src}" alt="" />
        {/if}
        {#if mainFish['Image Gallery'] && mainFish['Image Gallery'][0]}
        <img class="photo-img" src="{mainFish['Image Gallery'][0].src}" alt="" />
        {/if}
        {#if mainFish['Image Gallery'] && mainFish['Image Gallery'][1]}
        <img class="photo-img" src="{mainFish['Image Gallery'][1].src}" alt="" />
        {/if}
        {#if mainFish['Image Gallery'] && mainFish['Image Gallery'][2]}
        <img class="photo-img" src="{mainFish['Image Gallery'][2].src}" alt="" />
        {/if}
        {#if mainFish['Image Gallery'] && mainFish['Image Gallery'][3]}
        <img class="photo-img" src="{mainFish['Image Gallery'][3].src}" alt="" />
        {/if}
        {#if mainFish['Image Gallery'] && mainFish['Image Gallery'][4]}
        <img class="photo-img" src="{mainFish['Image Gallery'][4].src}" alt="" />
        {/if}

      </div>
    </div>
    <footer>
      <div class="notes">
        By Kyle Larson
      </div>
    </footer>
  </section>
</main>

<style>

nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

form {
  margin-right: 100px;
}

select {
  width: 100%;
  border: none;
  padding: 4px 8px;
  background-color: #f1f1f1;
  font-size: 16px;

  }


h1, h2, p {
  margin-top: 0;
}

header {
  background-color: black;
}

.site-name {
  color: white;
  padding: 15px 0 0px 35px; 
}

.hero {
  background-image: url('./grilled-fish-fillet.jpg');
  height: 200px;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

.title {
  background-color: black;
  display: inline-block;
  margin: 100px 0 20px 20px;
}

.fishName {
  color: white;
  padding: 10px 20px;
  margin: 0;
  text-shadow: 1px 2px 2px #333;
  font-size: 40px;
}

.container {
  display: grid;
  grid-template-columns: 6fr 1fr;
  margin: 10px 0 0 40px;
  width: 90vw;
}


.photo-img {
  margin: 10px 40px 40px 0px;
  border-radius: 5px;
  box-shadow: 2px 2px 2px #333;
  height: 200px;
}

.photo-group {
  grid-column: 1 / 4;
}

footer {
  background-color: black;
  height: 60px;
}

.notes {
  text-align: center;
  color: white;
  padding-top: 20px;

}

@media (max-width: 1000px) {
  .fishName {
    font-size: 22px;
  }
  form {
    margin-left: 20px;
    margin-right: 10px;
    
  }

  .photo-img {
    margin: 10px 40px 40px 0px;
    border-radius: 5px;
    box-shadow: 2px 2px 2px #333;
    height: 150px;
  }
}
</style>