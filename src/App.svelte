<script lang="ts">
  let notionPageText = "";
  let isTextFile = true;
  let files: FileList | null = null;

  $: if (files) {
    const file = files[0];

    console.log(`${file.name}: ${file.size} bytes`);
    const reader = new FileReader();

    reader.addEventListener(
      "load",
      () => {
        const res = reader.result as string;
        notionPageText = res;
      },
      false
    );

    if (file) {
      reader.readAsText(file);
    }
  }
</script>

<main>
  <div
    class="w-full min-h-screen flex flex-col items-center justify-center gap-10 p-16 bg-gradient-to-br from-rose-500 to-amber-400"
  >
    <h1 class="text-center text-6xl font-black text-white leading-tight">
      Convert your Notion Page<br /> to Astro 🚀
    </h1>

    <h2 class="text-4xl font-semibold text-white">Get Started Now</h2>

    <input accept="text/markdown" bind:files type="file" />

    <button class="text-white bg-indigo-500 px-4 py-2 rounded-lg"
      >Upload Page</button
    >

    <p>{notionPageText}</p>

    {#if !isTextFile}
      <p class="text-white text-xl">
        Please upload a text file (.md, .mdx, .txt)
      </p>
    {/if}
  </div>
</main>
