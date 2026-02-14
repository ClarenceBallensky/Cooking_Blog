<script lang=ts>
    import * as Select from "$lib/components/ui/select/index.js";
    
    const variations = [
        { value: "gcheese", label: "Sandwhich"},
        { value: "ques", label: "Loaded Quesadilla"}
    ];

    let value = $state("");

    const triggerContent = $derived(
        variations.find((f) => f.value === value)?.label ?? "Select your favorite"
    );
</script>

<div class="p-6">
   <h1 class="mb-6">Clarence's Cooking Blog</h1>

    <div class="p-4 bg-white/80 rounded-lg">

       <img src="/images/Delicious_Sandwich.jpg" 
             alt="Delicious Sandwhich" 
              class="w-64 rounded-lg float-left mr-6 mb-4" 
        />

        <p class="leading-relaxed wrap-break-words">
            Whether you prefer a sandwhich or a quesadilla, the end result is the same: a complete meal containing all essential food groups. 
            I start by frying up a simple quesadilla or grilled cheese in the pan. For quesadillas, I use a Mexican cheese blend, and for 
            sandwhiches, I use swiss cheese. Optionally, fry an egg sunny-side up to add in later. 
            Once the quasadilla/grilled cheese is crispy and overflowing with gooey cheese, I open it up and start stuffing it with extra 
            ingredients. This begin recipe will not only satisfy your appetite; it will boost your confidence, allowing you to progress 
            to more complex dishes. 
        </p>

        <Select.Root type="single" name="favoriteFruit" bind:value>
            <Select.Trigger class="w-45 text-base font-inherit">
                {triggerContent}
            </Select.Trigger>
            <Select.Content class="text-base font-inherit">
                <Select.Group>
                    <Select.Label>Variations</Select.Label>
                    {#each variations as variation (variation.value)}
                        <Select.Item
                            value={variation.value}
                            label={variation.label}
                        >
                            {variation.label}
                        </Select.Item>
                    {/each}
                </Select.Group>
            </Select.Content>
        </Select.Root>
   
    </div>
</div>


