<template>
    <div class="min-h-screen bg-white mx-48">
        <div class="flex">
            <!-- Left Section (Text) -->
            <div class="w-1/2 px-8 py-72 relative">
                <p class="text-xl text-gray-700 mb-4 h-[70vh] mx-36" ref="para1">
                    Lorem ipsum dolor sit amet consectetur adipisicing elit. Recusandae exercitationem possimus quos
                    illum,
                    nesciunt tempora, ullam aut, asperiores nostrum ab amet nobis repudiandae voluptates. Quo dicta nam
                    accusantium cupiditate recusandae. Lorem ipsum dolor sit amet consectetur adipisicing elit. Nulla
                    minus ad hic fugiat, quae at, eligendi earum vel sequi, architecto ipsum consequatur. Optio libero
                    error nemo, nam ducimus sit? Culpa!
                </p>
                <p class="text-xl text-gray-700 mb-4 h-[70vh] mx-36" ref="para2">
                    Lorem ipsum dolor, sit amet consectetur adipisicing elit. Iusto, tempore ab dolorum consequatur,
                    saepe nam
                    non doloribus porro inventore libero obcaecati mollitia amet, nisi qui laborum magnam. Voluptates,
                    ipsa
                    quaerat. Lorem ipsum dolor sit amet, consectetur adipisicing elit. Sunt quae quos deleniti eius
                    similique recusandae fugiat, cumque temporibus earum quibusdam autem! Nisi accusantium accusamus
                    laborum sed assumenda repudiandae quibusdam ipsa!
                </p>
                <p class="text-xl text-gray-700 mb-4 h-[70vh] mx-36" ref="para3">
                    Lorem, ipsum dolor sit amet consectetur adipisicing elit. Ab dignissimos voluptas molestiae, nisi
                    laborum
                    debitis fugiat optio velit iure? Iusto ullam dolores debitis enim reiciendis suscipit distinctio
                    dolorem
                    excepturi veritatis! Lorem ipsum dolor sit amet consectetur adipisicing elit. Excepturi quia debitis
                    animi officia, eveniet fugiat sit iste possimus porro voluptatum? Distinctio inventore reprehenderit
                    laboriosam minus numquam qui recusandae repudiandae nam.
                </p>
            </div>

            <!-- Right Section (Images) -->
            <div class="relative">
                <img ref="image1" src="/image.jpg" alt="Image 1"
                    class="object-cover w-[800px] h-[800px] fixed bottom-0" />
                <img ref="image2" src="/image2.jpg" alt="Image 2"
                    class="object-cover w-[800px] h-[800px] fixed opacity-0 bottom-0" />
                <img ref="image3" src="/image3.jpg" alt="Image 3"
                    class="object-cover w-[800px] h-[800px] fixed opacity-0 bottom-0" />
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "ScrollPage",
    mounted() {
        // Add scroll event listener
        window.addEventListener("scroll", this.handleScroll);
    },
    beforeDestroy() {
        // Remove the event listener
        window.removeEventListener("scroll", this.handleScroll);
    },
    methods: {
        handleScroll() {
            const image1 = this.$refs.image1;
            const image2 = this.$refs.image2;
            const image3 = this.$refs.image3;
            const para2 = this.$refs.para2;
            const para3 = this.$refs.para3;

            if (!image1 || !image2 || !image3 || !para2 || !para3) return;

            // Get positions of paragraphs relative to the viewport
            const para2Top = para2.getBoundingClientRect().top;
            const para3Top = para3.getBoundingClientRect().top;

            // Logic to transition between images based on scroll position
            if (para2Top < window.innerHeight / 2 && para3Top > window.innerHeight / 2) {
                // Show second image
                image1.style.opacity = "0";
                image2.style.opacity = "1";
                image3.style.opacity = "0";
            } else if (para3Top < window.innerHeight / 2) {
                // Show third image
                image1.style.opacity = "0";
                image2.style.opacity = "0";
                image3.style.opacity = "1";
            } else {
                // Show first image
                image1.style.opacity = "1";
                image2.style.opacity = "0";
                image3.style.opacity = "0";
            }

            // Smooth transitions
            image1.style.transition = "opacity 1s ease";
            image2.style.transition = "opacity 1s ease";
            image3.style.transition = "opacity 1s ease";
        },
    },
};
</script>

<style scoped>
img[ref="image"] {
    position: fixed;
    top: 50px;
    /* Adjust if needed */
    left: 50px;
    z-index: 10;
    opacity: 1;
    transition: opacity 1s ease;
}

img[ref="secondImage"] {
    position: fixed;
    top: 50px;
    /* Align with the first image */
    left: 50px;
    z-index: 5;
    opacity: 0;
    transition: opacity 1s ease;
}
</style>