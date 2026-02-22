<script lang=ts>
    import * as Select from "$lib/components/ui/select/index.js"; //select box for sandwich / quesadilla
    import { Checkbox } from "$lib/components/ui/checkbox/index.js"; //checkbox for poke bowl 
    import { Label } from "$lib/components/ui/label/index.js"; //label as a component of checkbox for poke bowl
    import { Button } from "$lib/components/ui/button/index.js"; //button for submitting poke bowl selections 
    
    // start sandwich select box
    const variations = [
        { value: "gcheese", label: "Sandwich"},
        { value: "ques", label: "Loaded Quesadilla"}
    ];

    let value = $state(""); //selected value 

    const triggerContent = $derived(
        variations.find((f) => f.value === value)?.label ?? "Select your favorite"
    );
    // end sandwich select box 

    // start poke bowl checkboxes

    let showResults = $state(false);

    let proteins = $state<string[]>([]);
    let toppings = $state<string[]>([]);
    let sauces = $state<string[]>([]);

    let itemSelected = $state(false);


    $effect(() => {
        proteins;
        toppings;
        sauces;

        showResults = false;
    });

    function toggleItem(list: string[], value: string) {
    return list.includes(value)
        ? list.filter(v => v !== value)
        : [...list, value];
    }

    const ALL_PROTEINS = ["salmon", "tuna", "tofu"];
    const ALL_TOPPINGS = ["mukimame", "pineapple", "seaweed", "crisps", "avocado"];
    const ALL_SAUCES   = ["eel_sauce", "spicy_mayo_sauce", "sriracha_sauce"];

  

    let isEnthusiast = $derived(
        proteins.length === ALL_PROTEINS.length &&
        toppings.length === ALL_TOPPINGS.length &&
        sauces.length   === ALL_SAUCES.length
    );

    let noneSelected = $derived(
        proteins.length === 0 &&
        toppings.length === 0 &&
        sauces.length   === 0
    );

    let isProteinLover = $derived(
        proteins.length === ALL_PROTEINS.length
    );

    let isSpiceLover = $derived(
        sauces.includes("sriracha_sauce")
    );

    let isToppingsLover = $derived(
        toppings.length == ALL_TOPPINGS.length 
    );

    let isVegetarian = $derived(
        !proteins.includes("salmon") &&
        !proteins.includes("tuna")
    );

    

   
    // end poke bowl checkboxes
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
                    src="/images/Sandwich_and_Quesadilla_MediumSize.jpeg" 
                    alt="Sandwich and Quesadilla" 
                    class="w-90 rounded-sm float-left mr-6 mb-4" 
                />

                <p class="leading-relaxed mb-4 mr-4">
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

            <!-- Poke Bowl -->
            <div class="mb-10"> 
                <h2 id="poke_bowl" class="py-4">Poke Bowl</h2>

                <div class="flex gap-6 items-start"> <!-- this div allows me to put checkboxes to the right of the image instead of beneath it -->
                    <!-- image -->
                    <div class="flex-shrink-0">
                        <img 
                            src="/images/Poke_Bowl.jpg"
                            alt="Poke Bowl"
                            class="rounded-lg w-90"
                        />
                    </div>


                    <div class="flex flex-col gap-6"> <!-- wrapper for checkboxes AND button -->

                        <div>
                            <h2 class="mb-4">Poke Bowl Personality Test!</h2>
                            <p>Create your dream poke bowl, and I'll tell you what it says about you.</p>
                        </div>

                        <!-- checkboxes -->
                        <div class="flex gap-6 items-start"> <!-- wrapper for checkboxes -->

                            <!-- protein-->
                            <div class="flex flex-col gap-6">
                                <h3 class="mb-2">Protein</h3>
                                <div class="flex flex-col gap-6">
                                    <div class="flex items-center gap-3">
                                        <Checkbox id="salmon"
                                                  checked={proteins.includes("salmon")}
                                                  onCheckedChange={(checked) => 
                                                    proteins = checked
                                                        ? [...proteins, "salmon"]
                                                        : proteins.filter(p => p !== "salmon")
                                                  }
                                        />
                                        <Label for="salmon">Salmon</Label>
                                    </div>
                                    <div class="flex items-start gap-3">
                                        <Checkbox id="tuna"
                                                  checked={proteins.includes("tuna")}
                                                  onCheckedChange={(checked) =>
                                                    proteins = checked
                                                        ? [...proteins, "tuna"]
                                                        : proteins.filter(p => p !== "tuna")
                                                  }
                                        />
                                        <Label for="tuna">Tuna</Label>
                                    </div>
                                    <div class="flex items-start gap-3">
                                        <Checkbox id="tofu" 
                                                  checked={proteins.includes("tofu")}
                                                  onCheckedChange={(checked) =>
                                                    proteins = checked
                                                        ? [...proteins, "tofu"]
                                                        : proteins.filter(p => p !== "tofu")
                                                  }
                                        />
                                        <Label for="tofu">Tofu</Label>
                                    </div>
                                </div>
                            </div>

                            <!-- toppings -->
                            <div class="flex flex-col gap-6">
                                <h3 class="mb-2">Toppings</h3>
                                <div class="flex flex-col gap-6">
                                    <div class="flex items-start gap-3">
                                        <Checkbox id="mukimame" 
                                                  checked={toppings.includes("mukimame")}
                                                  onCheckedChange={(checked) =>
                                                    toppings = checked
                                                        ? [...toppings, "mukimame"]
                                                        : toppings.filter(p => p !== "mukimame")
                                                  }
                                        />
                                        <div class="grid gap-2">
                                            <Label for="mukimame">Mukimame</Label>
                                            <p class="text-muted-foreground text-sm">
                                                Mukimame is the Japanese term for
                                            </p>
                                            <p class="text-muted-foreground text-sm">
                                                shelled edamame 
                                            </p>
                                        </div>
                                    </div>
                                    <div class="flex items-start gap-3">
                                        <Checkbox id="pineapple" 
                                                  checked={toppings.includes("pineapple")}
                                                  onCheckedChange={(checked) =>
                                                    toppings = checked
                                                        ? [...toppings, "pineapple"]
                                                        : toppings.filter(p => p !== "pineapple")
                                                  }
                                        />
                                        <Label for="pineapple">Pineapple</Label>
                                    </div>
                                    <div class="flex items-start gap-3">
                                        <Checkbox id="seaweed" 
                                                  checked={toppings.includes("seaweed")}
                                                  onCheckedChange={(checked) =>
                                                    toppings = checked
                                                        ? [...toppings, "seaweed"]
                                                        : toppings.filter(p => p !== "seaweed")
                                                  }
                                        />
                                        <Label for="seaweed">Seaweed Salad</Label>
                                    </div>
                                    <div class="flex items-start gap-3">
                                        <Checkbox id="crisps" 
                                                  checked={toppings.includes("crisps")}
                                                  onCheckedChange={(checked) =>
                                                    toppings = checked
                                                        ? [...toppings, "crisps"]
                                                        : toppings.filter(p => p !== "crisps")
                                                  }/>
                                        <Label for="crisps">Tempura Crisps</Label>
                                    </div>
                                    <div class="flex items-start gap-3">
                                        <Checkbox id="avocado" 
                                                  checked={toppings.includes("avocado")}
                                                  onCheckedChange={(checked) =>
                                                    toppings = checked
                                                        ? [...toppings, "avocado"]
                                                        : toppings.filter(p => p !== "avocado")
                                                  }/>
                                        <Label for="avocado">Avocado</Label>
                                    </div>
                                </div>
                            </div>
                    
                            <!-- sauces -->
                            <div class="flex flex-col gap-6">
                                <h3 class="mb-2">Sauces</h3>
                                <div class="flex flex-col gap-6">
                                    <div class="flex items-start gap-3">
                                        <Checkbox id="eel_sauce" 
                                                  checked={sauces.includes("eel_sauce")}
                                                  onCheckedChange={(checked) =>
                                                    sauces = checked
                                                        ? [...sauces, "eel_sauce"]
                                                        : sauces.filter(p => p !== "eel_sauce")
                                                  }
                                        />
                                        <Label for="eel_sauce">Eel Sauce</Label>
                                    </div>
                                    <div class="flex items-start gap-3">
                                        <Checkbox id="spicy_mayo_sauce" 
                                                  checked={sauces.includes("spicy_mayo_sauce")}
                                                  onCheckedChange={(checked) =>
                                                    sauces = checked
                                                        ? [...sauces, "spicy_mayo_sauce"]
                                                        : sauces.filter(p => p !== "spicy_mayo_sauce")
                                                  }
                                        />
                                        <Label for="spicy_mayo_sauce">Spicy Mayo</Label>
                                    </div>
                                    <div class="flex items-start gap-3">
                                        <Checkbox id="sriracha_sauce" 
                                                  checked={sauces.includes("sriracha_sauce")}
                                                  onCheckedChange={(checked) =>
                                                    sauces = checked
                                                        ? [...sauces, "sriracha_sauce"]
                                                        : sauces.filter(p => p !== "sriracha_sauce")
                                                  }
                                        />
                                        <Label for="sriracha_sauce">Sriracha</Label>
                                    </div>
                                </div>
                            </div>
                        </div>

                        <div> <!-- wrapper for button -->
                            <!-- button -->
                            <Button size="sm" 
                                    onclick={() => showResults = true}
                            >
                                Get my results!
                            </Button>
                        </div>

                        {#if showResults} <!-- once button is clicked -->
                            {#if isEnthusiast}
                                <h3>The Enthusiast! 💗</h3>
                                <p>You say yes to everything--even when you shouldn't. You're adventerous and outgoing,
                                    and people can't help but gravitate towards you when you walk into a room. Your open-mindedness 
                                    allows you to connect with people from all different backgrounds. Keep living your best life.
                                </p>
                            {:else if noneSelected}
                                <h3>The Minimalist... 💀</h3>
                                <p>Maybe you're not hungry right now, or maybe you wanted to see what my website would do if you
                                    made no selections whatsoever then clicked the button. You're not one to let The Man boss you around.
                                    You're a curious person with strong beliefs; seeing is believing. You may sit at the back of the class,
                                    but you're listening to every word. Stay spunky. 
                                </p>
                            {:else if isProteinLover}
                                <h3 class="pt-7">The Protein Lover! 💪</h3>
                                <p>You wouldn't skip a day at the gym if zombies were roaming the streets. You are diligent and 
                                    hardworking. You know that you owe yourself your best every day, and you continously strive 
                                    for self improvement. Your loved ones see the hard work you put in everyday, and they are 
                                    proud of you.
                                </p>
                            {:else if isSpiceLover}
                                <h3>The Spice Lover! 🌶️</h3>
                                <p>You were never one to turn down a dare; you like to live life on the edge,
                                   keep things exciting. Maybe you've tried out bungey jumping or skydiving. Or
                                   maybe you dance extra crazy at the club. Whatever the case may be, your friends
                                   know they can count on you for a good time. 
                                </p>
                            {:else if isToppingsLover}
                                <h3>The Toppings Lover! 🥗</h3>
                                <p>Why would you settle for less when you could live life to it's fullest? Your optimism about life is attractive
                                    to strangers and friends alike. Your can-do energy will bring you success in your career and personal life,
                                    affording you opportunities wherever you go. Staying active will ensure you keep your youthful glow even as 
                                    you age.   
                                </p>
                            {:else if isVegetarian}
                                <h3>The Vegetarian! 🌿</h3>
                                <p>Maybe you don't like the thought of hurting animals, or maybe the thought of raw
                                    fish just grosses you out. Either way, you are a thoughtful and introspective person. You take the 
                                    time to notice the things that others miss. You have the patience to work on projects to completion,
                                    always putting your best foot forward. Tranquility is your strength. 
                                </p>
                            {:else}
                                <h3>The Crowd Pleaser 😎</h3>
                                <p>You are the ultimate team player, always willing to go with the flow. Your laid back attitude makes your
                                    friends and coworkers feel at ease when they're around you. You're the perfect person to chill with on
                                    a Sunday afternoon. Your openness to different kinds of opportunites gives you a well-rounded perspective on
                                    life. Stay cool. 
                                </p>
                            
                            {/if}
                            


                        {/if}


                    </div>

                </div>

            </div>
            
            <!-- Persian Kebab Section -->
            <div class="mb-10"> 
                <h2 id="kebab" class="py-4">Persian Kebab</h2>

                <img 
                    src="/images/Persian_Kebab.jpg"
                    alt="Persian Kebab"
                    class="rounded-lg w-64"
                />

                <p class="leading-relaxed mb-4">

                </p>

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


