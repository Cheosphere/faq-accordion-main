<script setup>
import { ref, onMounted } from 'vue'

const faqs = ref([
    {
        title: 'What is Frontend Mentor, and how will it help me?',
        answer: "Frontend Mentor offers realistic coding challenges to help developers improve their frontend coding skills with projects in HTML, CSS, and JavaScript. It's suitable for all levels and ideal for portfolio building.",
        isOpen: true
    },
    {
        title: 'Is Frontend Mentor free?',
        answer: 'Yes, Frontend Mentor offers both free and premium coding challenges, with the free option providing access to a range of projects suitable for all skill levels.',
        isOpen: false
    },
    {
        title: 'Can I use Frontend Mentor projects in my portfolio?',
        answer: "Yes, you can use projects completed on Frontend Mentor in your portfolio. It's an excellent way to showcase your skills to potential employers!",
        isOpen: false
    },
    {
        title: "How can I get help if I'm stuck on a challenge?",
        answer: "The best place to get help is inside Frontend Mentor's Discord community. There's a help channel where you can ask questions and seek support from other community members.",
        isOpen: false
    }
])

const isOpen = ref(false)

function toggleAccordion(index) {
    faqs.value.forEach(item => {
        if (item.isOpen === true) {
            item.isOpen = false
        }
    })
    faqs.value[index].isOpen = !faqs.value[index].isOpen
}

const currentQuestion = ref(0)

onMounted(() => {
    const handleKeyDown = (event) => {
        const number = ref(0)
        switch (event.key) {
            case 'ArrowUp':
                if (currentQuestion.value > 0) {
                    number.value = currentQuestion.value - 1
                    toggleAccordion(number.value)
                    currentQuestion.value = number.value
                }
                break
            case 'ArrowDown':
                if (currentQuestion.value <= 2) {
                    number.value = currentQuestion.value + 1
                    toggleAccordion(number.value)
                    currentQuestion.value = number.value
                }
                break
            default:
                break
        }
    }

    window.addEventListener('keydown', handleKeyDown)

    return () => {
        window.removeEventListener('keydown', handleKeyDown)
    }
})


</script>

<template>
    <figure class="bg"></figure>
    <section class="container">
        <header class="header">
            <figure>
                <img src="./assets/images/icon-star.svg" alt="icon star">
            </figure>
            <h1 class="header-title">FAQs</h1>
        </header>
        <main class="content">
            <article class="faqs" @click="toggleAccordion(index)" v-for="(faq, index) in faqs" :key="index">
                <div class="faqs-header">
                    <h3 class="faqs-title">{{ faq.title }}</h3>
                    <figure v-if="faq.isOpen" class="faqs_close_icon"></figure>
                    <figure v-else class="faqs-icon"></figure>
                </div>
                <p v-if="faq.isOpen" class="faqs-content">{{ faq.answer }}</p>
            </article>
        </main>
    </section>
</template>

<style scoped>
.bg {
    width: 100%;
    height: 320px;
    position: absolute;
    background-image: url('./assets/images/background-pattern-desktop.svg');
    background-repeat: no-repeat;
    background-size: cover;
    z-index: -10;
}

.container {
    width: 95%;
    max-width: 600px;
    min-height: 566px;
    padding: 2.3rem;
    display: flex;
    flex-direction: column;
    align-self: center;
    border-radius: 1rem;
    background-color: var(--white);
    box-shadow: 0px 30px 60px rgba(0, 0, 0, 0.1);
}

.header {
    display: flex;
    align-items: center;
}

.header-title {
    margin-left: 1.5rem;
    font-size: 3.5rem;
    position: relative;
    bottom: .15rem;
}

.content {
    width: 100%;
    margin-top: 1rem;
    transition: height 0.5s ease;
}

.faqs {
    height: auto;
    padding: 1.4rem 0;
    border-bottom: 1px solid rgba(211, 211, 211, 0.4);
}

.faqs:last-of-type {
    border-bottom: none;
}

.faqs-header {
    width: 100%;
    display: flex;
    justify-content: space-between;
    align-items: center;
    cursor: pointer;
}

.faqs-title {
    font-size: 1.12rem;
    font-weight: 600;
    color: var(--dark-purple);
    transition: .3s;
}

.faqs-title:hover {
    color: #ad28eb;
}

.faqs-icon {
    min-width: 30px;
    min-height: 30px;
    margin-left: 1rem;
    background-image: url('./assets/images/icon-plus.svg');
    background-position: center;
    background-size: cover;
}

.faqs_close_icon {
    min-width: 30px;
    min-height: 30px;
    margin-left: 1rem;
    background-image: url('./assets/images/icon-minus.svg');
    background-position: center;
    background-size: cover;
}

.faqs-content {
    margin-top: 1.45rem;
    font-size: 1.02rem;
    font-weight: 300;
    letter-spacing: .018rem;
    line-height: 1.5rem;
    color: var(--grayish-purple);
}

/* Media Query */
@media screen and (max-width: 580px) {
    .bg {
        width: 100%;
        height: 232px;
        background-image: url('./assets/images/background-pattern-mobile.svg');
        background-repeat: no-repeat;
        background-size: cover;
    }

    .container {
        padding: 1.5rem;
    }

    .faqs-title {
        margin-right: 1rem;
    }
}

@media screen and (max-width: 480px) {
    .header img {
        width: 30px;
    }

    .header-title {
        margin-left: 1.5rem;
        font-size: 2.5rem;
        position: relative;
        bottom: .15rem;
    }

    .faqs-title {
        font-size: 1rem;
    }

    .faqs-content {
        font-size: 1rem;
    }
}

@media screen and (max-width: 374px) {
    .faqs-title {
        margin: 0;
    }
}
</style>
