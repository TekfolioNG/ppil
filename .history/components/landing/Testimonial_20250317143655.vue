<template>
    <div class="testimonial-section">
        <div class="content-container">
            <div class="testimonial-image-container">
                <img src="@/assets/img/toei-testimonial.jpg" alt="Testimonial portrait" class="testimonial-image">
            </div>
            <div class="testimonial-content">
                <div class="quote-mark">
                    <svg width="40" height="32" viewBox="0 0 40 32" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path
                            d="M0 32V20C0 17.6 0.466667 15.3333 1.4 13.2C2.33333 11 3.6 9.06667 5.2 7.4C6.8 5.73333 8.6 4.4 10.6 3.4C12.6667 2.33333 14.8 1.66667 17 1.4L18.2 5.8C15.6667 6.33333 13.4 7.46667 11.4 9.2C9.46667 10.9333 8.33333 13.2667 8 16.2H16V32H0ZM22 32V20C22 17.6 22.4667 15.3333 23.4 13.2C24.3333 11 25.6 9.06667 27.2 7.4C28.8 5.73333 30.6 4.4 32.6 3.4C34.6667 2.33333 36.8 1.66667 39 1.4L40.2 5.8C37.6667 6.33333 35.4 7.46667 33.4 9.2C31.4667 10.9333 30.3333 13.2667 30 16.2H38V32H22Z"
                            fill="#1FAE94" />
                    </svg>
                </div>
                <p class="testimonial-text">
                    The education program has opened doors I never thought possible.
                    From learning to read to now pursuing my dream of becoming a teacher,
                    this journey has transformed not just my future, but my entire family's
                    outlook on what's possible.
                </p>
                <div class="testimonial-attribution">
                    <span class="name">— MARIA, 21, SPONSORED SINCE AGE 7, ECUADOR</span>
                    <a href="#" class="read-more">READ HER STORY <span class="arrow">›</span></a>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'TestimonialSection'
}
</script>

<style scoped>
.testimonial-section {
    background-color: #f5f5f5;
    padding: 3rem 0;
    width: 100%;
}

.content-container {
    width: 60%;
    margin: 0 auto;
    display: flex;
    align-items: center;
    gap: 2.5rem;
}

.testimonial-image-container {
    flex-shrink: 0;
    width: 220px;
    height: 220px;
    border-radius: 50%;
    overflow: hidden;
}

.testimonial-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.testimonial-content {
    flex-grow: 1;
    position: relative;
}

.quote-mark {
    color: #1FAE94;
    margin-bottom: 0.5rem;
}

.testimonial-text {
    font-size: 1.5rem;
    line-height: 1.5;
    color: #1FAE94;
    margin-bottom: 1.5rem;
    font-weight: 400;
}

.testimonial-attribution {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-top: 1rem;
}

.name {
    font-size: 0.9rem;
    font-weight: 500;
    color: #1FAE94;
    letter-spacing: 0.5px;
}

.read-more {
    font-size: 0.85rem;
    font-weight: 600;
    color: #1FAE94;
    text-decoration: none;
    display: flex;
    align-items: center;
    transition: all 0.2s ease;
}

.read-more:hover {
    opacity: 0.8;
}

.arrow {
    margin-left: 0.25rem;
    font-size: 1.2rem;
}

@media (min-width: 1400px) {
    .content-container {
        width: 60%;
    }
}

@media (max-width: 1399px) {
    .content-container {
        width: 70%;
    }
}

@media (max-width: 992px) {
    .content-container {
        width: 80%;
    }
}

@media (max-width: 768px) {
    .content-container {
        width: 85%;
        flex-direction: column;
        text-align: center;
        gap: 1.5rem;
    }

    .testimonial-image-container {
        width: 180px;
        height: 180px;
    }

    .testimonial-text {
        font-size: 1.3rem;
    }

    .testimonial-attribution {
        flex-direction: column;
        gap: 0.75rem;
    }

    .quote-mark {
        text-align: center;
    }
}

@media (max-width: 480px) {
    .content-container {
        width: 90%;
    }

    .testimonial-image-container {
        width: 150px;
        height: 150px;
    }

    .testimonial-text {
        font-size: 1.2rem;
    }
}
</style>