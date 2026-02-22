<script lang=ts>
    import * as Accordion from "$lib/components/ui/accordion/index.js";
</script>

<div class="p-6">
    <h1 class="mb-6">About Me</h1>

    <div class="flex gap-8 mt-6 items-start">
          
        <div class="p-4 bg-white/80 rounded-lg">

            <img
                src="/images/My_Face.jpeg"
                alt="Picture of Me"
                class="w-100 rounded-sm float-left mr-6 mb-4" 
            />

            <h2 class="mb-4">Nice to Meet You!</h2>

            <p class="leading-relaxed mb-4">
                The first time I turned on the electric stove in my college dorm room, I set off the fire alarm. My roommates weren't exactly pleased.
                I was in my sophomore year, I was sick of the food at the college cafeteria, and I was excited to try something new.
            </p>

            <p class="leading-relaxed mb-4"> Since that unfortunate incident, I have continued refining my culinary skills--attempting to 
                replicate a variety of cuisines from around the globe. I consider every cooking failure a benchmark in my progress; these 
                are the necesary growing pains of improving my craft. 
            </p>

            <p class="leading-relaxed mb-4">
                As a computer science major, I developed this website to merge my passion for cooking with my technical background, serving as 
                both a creative outlet and a demonstration of my coding skills. 
            </p>

            <h3 class="mb-4">Q&A</h3>

            <Accordion.Root type="single" class="w-full sm:max-w-[70%]">
                <Accordion.Item value="item-1">
                    <Accordion.Trigger>Do you have any cooking tips?</Accordion.Trigger>
                    <Accordion.Content class="flex flex-col gap-4 text-balance">
                        <p>
                            Yes! If you like rice, invest in a rice cooker. It saves you the stress, and your rice will come out soft 
                            and fluffy every time. 
                        </p>
                    </Accordion.Content>
                </Accordion.Item>
                <Accordion.Item value="item-2">
                    <Accordion.Trigger>Where do you go to find new recipes?</Accordion.Trigger>
                    <Accordion.Content class="flex flex-col gap-4 text-balance">
                        <p>
                            Pinterest. I like that I can scroll through pictures of finished meals—scanning for the tastiest version. 
                            Pinterest also allows me to quickly save and access saved recipes. #notsponsored
                        </p>
                    </Accordion.Content>
                </Accordion.Item>
                 <Accordion.Item value="item-3">
                    <Accordion.Trigger>What is your favorite dish to make?</Accordion.Trigger>
                    <Accordion.Content class="flex flex-col gap-4 text-balance">
                        <p>
                            I love making basil pesto pasta with pine nuts and lemon chicken. It's my go-to dish to impress friends and family.
                        </p>
                    </Accordion.Content>
                </Accordion.Item>
            </Accordion.Root>
        
 
        </div>

    </div>

</div>