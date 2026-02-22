<script lang=ts>
    import * as Select from "$lib/components/ui/select/index.js";
    
    const variations = [
        { value: "gcheese", label: "Sandwich"},
        { value: "ques", label: "Loaded Quesadilla"}
    ];

    let value = $state(""); //selected value 

    const triggerContent = $derived(
        variations.find((f) => f.value === value)?.label ?? "Select your favorite"
    );
</script>

<div class="p-6">
   <h1 class="mb-6">Clarence's Cooking Blog</h1>

   <div class="flex gap-8 mt-6 items-start">

        <!-- main page (left side) -->
        <div class="p-4 bg-white/80 rounded-lg">

            <!-- Sandwhich/Quesdilla Section-->
            <div class="mb-10">
                <h2 id="sandwich_quesadilla" class="py-4">Sandwich / Loaded Quesadilla</h2>
                
                <img 
                    src="/images/Sandwich_and_Quesadilla.jpg" 
                    alt="Sandwich and Quesadilla" 
                    class="w-80 rounded-sm float-left mr-6 mb-4" 
                />

                <p class="leading-relaxed mb-4">
                    During my first year of college, I spent most of my time in two places: my dorm room, and the cafeteria. The cafetaria wasn't just 
                    my best option for a filling meal; it was a place to make new friends, study, and hang out in-between classes. However, as grateful
                    as I am for my freshman year cafeteria experience, it quickly came to my attention that the food was, well, diabolical. I was spoiled on my
                    mom's home-cooking; cardboard pizza and undercooked rice weren't making the cut. Problem was, I had no cooking
                    experience. When I told my mom I wanted to start cooking, she reminded me that I couldn't even toast bread 
                    without burning it. (She was right, unfortunately.) If I wanted to cook, I'd have to start with the basics. And what could be more 
                    basic than a sandwich? It's quick, it's easy, and it contains all essential foodgroups. The perfect starter meal.
                    Start by frying up a simple quesadilla or grilled cheese in the pan. Optionally, fry an egg sunny-side up to add in later. 
                    Once the quasadilla/grilled cheese is crispy and overflowing with gooey cheese, I open it up and start stuffing it with extra 
                    ingredients. This beginner recipe will not only satisfy your appetite; it will boost your confidence, allowing you to progress 
                    to more complex dishes. 
                </p>

                <div class="clear-both"></div>

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


                {#if value}
                    <div class="flex gap-8 mt-6 items-start">
                        
                        <!-- bullet point ingredients -->
                        <div>
                            <!-- quesadilla-specific ingredients -->  
                            {#if value == "ques"}
                                <ul class="list-disc pl-6 space-y-1"> 
                                    <li>flour tortilla</li>
                                    <li>mexican cheese</li>
                                </ul>
                            {/if}

                            <!-- sandwich-specific ingredients -->
                            {#if value == "gcheese"}
                                <ul class="list-disc pl-6 space-y-1">
                                    <li>white or potato bread</li>
                                    <li>swiss cheese</li>
                                </ul>
                            {/if}

                            <!-- shared ingredients -->
                            {#if value }
                                <ul class="list-disc pl-6 space-y-1"> 
                                    <li>roma tomato</li>
                                    <li>spinach</li>
                                    <li>egg</li>
                                    <li>turkey lunch meat</li>
                                    <li>ham lunch meat</li>
                                    <li>vegetable oil</li>
                                    <li>salt</li>
                                    <li>pepper</li>
                                </ul>
                            {/if}
                        </div>

                        <!-- sandwich or quesadilla image 1, corresponding to user choice  -->
                        <div class="w-64 flex-shrink-0">
                            {#if value == "ques"}
                                <img
                                    src="/images/Just_a_Quesadilla.jpeg"
                                    alt="Quesadilla"
                                    class="rounded-lg w-64"
                                />
                            {/if}

                            {#if value == "gcheese"}
                                <img
                                    src="/images/Just_a_Sandwich.jpeg"
                                    alt="Sandwich"
                                    class="rounded-lg w-64"
                                />
                            {/if}
                        </div>

                        <!-- sandwich or quesadilla image 2, corresponding to user choice  -->
                        <div>
                            {#if value == "ques"}
                                <img
                                    src="/images/Quesadilla_Ingredients.jpeg"
                                    alt="Quesadilla Ingredients"
                                    class="rounded-lg w-130"
                                />
                            {/if}

                            {#if value == "gcheese"}
                                <img
                                    src="/images/Sandwich_Ingredients.jpeg"
                                    alt="Sandwich Ingredients"
                                    class="rounded-lg w-113"
                                />
                            {/if}
                        </div>


                    </div>
                {/if}
            </div>

            <!-- Poke Bowl Section -->
            <div class="mb-10"> 
                <h2 id="poke_bowl">Poke Bowl</h2>

                <img 
                    src="/images/Poke_Bowl.jpg"
                    alt="Poke Bowl"
                    class="rounded-lg w-64"
                />

            </div>
            
            <!-- Persian Kebab Section -->
            <div class="mb-10"> 
                <h2 id="kebab">Persian Kebab</h2>

                <img 
                    src="/images/Persian_Kebab.jpg"
                    alt="Persian Kebab"
                    class="rounded-lg w-64"
                />

            </div>

        </div>

        <!-- right margin of website, used for navigation -->
        <div class="w-64 flex-shrink-0">
            <h3 class="pb-4">Jump ahead!</h3>
            <a href="#sandwich_quesadilla" 
              class="hover:opacity-70">
                <h4>Sandwich / Quesadilla</h4>
                <img 
                    src="/images/Sandwich_and_Quesadilla_OriginalSize.jpeg" 
                    alt="Sandwich and Quesadilla" 
                    class="w-80 rounded-sm float-left mr-6 mb-4" 
                />
            </a>
            <a href="#poke_bowl"
               class="hover:opacity-70">
                <h4>Poke Bowl</h4>
                <img 
                    src="/images/Poke_Bowl.jpg" 
                    alt="Sandwich and Quesadilla" 
                    class="w-80 rounded-sm float-left mr-6 mb-4" 
                />
            </a>
            <a href="#kebab"
               class="hover:opacity-70">
                <h4>Persian Kebab</h4>
                <img 
                    src="/images/Persian_Kebab.jpg" 
                    alt="Sandwich and Quesadilla" 
                    class="w-80 rounded-sm float-left mr-6 mb-4" 
                />
            </a>
        </div>

    </div>

 

</div>


