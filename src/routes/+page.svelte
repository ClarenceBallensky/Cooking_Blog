

<div class="p-6">
    <h1 class="text-4xl font-bold mb-4">Clarence's Food Blog</h1>
    <p>{count}</p>
    <button type="button" class="bg-green-500 border-black border-2 rounded hover:bg-green-700" onclick={() => count++}>Increase Number</button>
    <button type="button" class="bg-red-500 border-black border-2 rounded hover:bg-red-700" onclick={() => count--}>Decrease Number</button>
    <p>Click <a class="text-blue-500 underline hover:text-blue-700" href="https://www.youtube.com/watch?v=dQw4w9WgXcQ&list=RDdQw4w9WgXcQ&start_radio=1">here</a> for fun button facts!</p>
</div>


<script lang=ts>
    let count: number=$state(0);
    let is4 = $derived(count == 4);
    $effect(() => {
        if (count === 100) {
            alert("fireworks");
        } 
    })
</script>