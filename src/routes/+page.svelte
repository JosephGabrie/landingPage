<script lang="ts">
  import { supabase } from "$lib/supabase";
  import { goto } from "$app/navigation";
  let email = "";
  let loading = false;
  let error = "";
  let totalCount = 0;
  async function fetchCount() {
    const { count, error: countError } = await supabase
      .from("waitlist")
      .select("*", { count: "exact", head: true });

    if (!countError && count !== null) {
      totalCount = count;
    }
  }

  fetchCount();

  async function handleSubmit() {
    error = "";

    if (!email.trim()) {
      error = "Please enter your email";
      return;
    }

    if (!email.includes("@")) {
      error = "Please enter a valid email address";
      return;
    }

    loading = true;

    const { error: insertError } = await supabase
      .from("waitlist")
      .insert([
        { name: email.split("@")[0], email: email.trim().toLowerCase() },
      ]);
    loading = false;

    if (insertError) {
      if (insertError.code === "23505") {
        error = "This email is already on the waitlist!";
      } else {
        error = "Something went wrong. Please try again.";
      }
    } else {
      goto("/Thanks");
    }
  }

  let openFaqIndex: number | null = null;

  function toggleFaq(index: number) {
    openFaqIndex = openFaqIndex === index ? null : index;
  }

  const faqs = [
    {
      question: "What is MiseEnCode?",
      answer:
        "MiseEnCode is a subscription service that delivers fully scoped project kits to your doorstep each month. Each kit includes design files, assets, requirements documentation, and everything you need to start coding immediately—no planning required.",
    },
    {
      question: "How does the subscription work?",
      answer:
        "Once subscribed, you'll receive a new project kit every month. Each kit is carefully curated with complete specifications, design mockups, assets, and detailed requirements so you can focus solely on the fun part: coding.",
    },
    {
      question: "What kind of projects will I receive?",
      answer:
        "Projects range from web applications and mobile apps to APIs and developer tools. Each project is designed to be completable within a reasonable timeframe while teaching you valuable development skills and modern technologies.",
    },
    {
      question: "Do I need to be an expert developer?",
      answer:
        "Not at all! Our project kits cater to various skill levels, from beginners to advanced developers. Each kit includes clear documentation and requirements that make it easy to understand what needs to be built.",
    },
    {
      question: "What's included in each kit?",
      answer:
        "Each kit contains: complete requirements documentation, design files and mockups, all necessary assets (images, icons, fonts), API specifications if needed, suggested tech stack, and bonus resources to help you succeed.",
    },
    {
      question: "When will the service launch?",
      answer:
        "We're currently building out our first collection of project kits. Join the waitlist to be notified as soon as we launch and get exclusive early access to our first kits.",
    },
    {
      question: "Will I get early access by joining the waitlist?",
      answer:
        "Yes! Waitlist members will receive priority access to our launch, special pricing, and bonus content when we go live.",
    },
  ];
</script>

<div class="landing-page">
  <div class="hero">
    <div class="container">
      <div class="logo-icon">
        <svg viewBox="0 0 24 24" fill="currentColor">
          <path
            d="M3 3h8v8H3V3zm10 0h8v8h-8V3zM3 13h8v8H3v-8zm10 0h8v8h-8v-8z"
          />
        </svg>
      </div>

      <div class="badge">
        <span class="dot"></span>
        AVAILABLE IN EARLY 2026
      </div>

      <h1 class="headline">Get early access<br />to MiseEnCode</h1>
      <p class="subheadline">
        Be amongst the first to experience Wait and launch a viral<br
          class="desktop-only"
        />
        waitlist. Sign up to be notified when we launch!
      </p>

      {#if totalCount > 0}
        <p class="counter">
          Join {totalCount.toLocaleString()}+ others on the waitlist
        </p>
      {/if}

      <form
        on:submit|preventDefault={handleSubmit}
        class="waitlist-form"
        action="https://submit-form.com/8wIZBVUvg"
      >
        <div class="form-row">
          <input
            type="email"
            placeholder="Email"
            bind:value={email}
            disabled={loading}
            required
          />
          <button type="submit" disabled={loading} class="cta-button">
            {loading ? "Joining..." : "Join waitlist"}
          </button>
        </div>
        {#if error}
          <p class="error">{error}</p>
        {/if}
      </form>
    </div>
  </div>

  <div class="faq">
    <div class="container">
      <h2>Frequently asked questions</h2>
      <p class="faq-subtitle">
        Everything you need to know about the Wait template. Find<br
          class="desktop-only"
        />
        answers to the most common questions below.
      </p>

      <div class="faq-list">
        {#each faqs as faq, index}
          <div class="faq-item">
            <button class="faq-question" on:click={() => toggleFaq(index)}>
              <span>{faq.question}</span>
              <span class="faq-toggle"
                >{openFaqIndex === index ? "−" : "+"}</span
              >
            </button>
            {#if openFaqIndex === index}
              <div class="faq-answer">
                <p>{faq.answer}</p>
              </div>
            {/if}
          </div>
        {/each}
      </div>
    </div>
  </div>
</div>

<style>
  .landing-page {
    min-height: 100vh;
    background: #fafafa;
  }

  .container {
    max-width: 900px;
    margin: 0 auto;
    padding: 0 20px;
  }

  .hero {
    padding: 80px 20px 120px;
    text-align: center;
  }
  .hero .container {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .logo-icon {
    width: 64px;
    height: 64px;
    background: #ffbe0b;
    border-radius: 16px;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 32px;
  }

  .logo-icon svg {
    width: 32px;
    height: 32px;
    color: #000;
  }

  .badge {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    font-size: 0.75rem;
    font-weight: 600;
    letter-spacing: 0.5px;
    color: #6b7280;
    margin-bottom: 32px;
    text-transform: uppercase;
  }

  .dot {
    width: 8px;
    height: 8px;
    background: #ffbe0b;
    border-radius: 50%;
  }

  .headline {
    font-size: 3.5rem;
    font-weight: 500;
    margin: 0 0 24px;
    line-height: 1.2;
    color: #111827;
    letter-spacing: -1px;
  }

  .subheadline {
    font-size: 1.125rem;
    line-height: 1.7;
    color: #6b7280;
    margin: 0 0 24px;
  }

  .counter {
    color: #6b7280;
    font-size: 0.95rem;
    margin: 0 0 32px;
  }

  .waitlist-form {
    max-width: 600px;
    margin: 0 auto 24px;
  }

  .form-row {
    display: flex;
    gap: 12px;
    align-items: flex-start;
  }

  input {
    flex: 1;
    padding: 16px 20px;
    border: 1px solid #e5e7eb;
    border-radius: 8px;
    font-size: 1rem;
    transition: all 0.2s ease;
    background: white;
    font-family: "DM Sans", sans-serif;
  }

  input:focus {
    outline: none;
    border-color: #ffbe0b;
    box-shadow: 0 0 0 3px rgba(255, 190, 11, 0.1);
  }

  input:disabled {
    background: #f9fafb;
    cursor: not-allowed;
  }

  .error {
    color: #ef4444;
    margin: 12px 0 0;
    font-size: 0.875rem;
    text-align: center;
  }

  .cta-button {
    padding: 16px 32px;
    background: #ffbe0b;
    color: #000;
    border: none;
    border-radius: 8px;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.2s ease;
    white-space: nowrap;
    font-family: "DM Sans", sans-serif;
  }

  .cta-button:hover:not(:disabled) {
    background: #e5ab09;
    transform: translateY(-1px);
    box-shadow: 0 4px 12px rgba(255, 190, 11, 0.3);
  }

  .cta-button:active:not(:disabled) {
    transform: translateY(0);
  }

  .cta-button:disabled {
    opacity: 0.6;
    cursor: not-allowed;
  }

  .faq {
    background: white;
    padding: 80px 20px 100px;
  }

  .faq h2 {
    text-align: center;
    font-size: 2.5rem;
    font-weight: 500;
    margin: 0 0 16px;
    color: #111827;
  }

  .faq-subtitle {
    text-align: center;
    color: #6b7280;
    font-size: 1.125rem;
    line-height: 1.7;
    margin: 0 0 60px;
  }

  .faq-list {
    max-width: 700px;
    margin: 0 auto;
  }

  .faq-item {
    border-bottom: 1px solid #e5e7eb;
    padding: 24px 0;
  }

  .faq-item:first-child {
    border-top: 1px solid #e5e7eb;
  }

  .faq-question {
    width: 100%;
    padding: 0;
    background: none;
    border: none;
    text-align: left;
    font-size: 1.125rem;
    font-weight: 500;
    color: #111827;
    cursor: pointer;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-family: "DM Sans", sans-serif;
  }

  .faq-toggle {
    font-size: 1.5rem;
    color: #6b7280;
    font-weight: 300;
    flex-shrink: 0;
    margin-left: 16px;
  }

  .faq-answer {
    padding-top: 16px;
    animation: slideDown 0.3s ease;
  }

  .faq-answer p {
    color: #6b7280;
    line-height: 1.7;
    margin: 0;
  }

  .desktop-only {
    display: inline;
  }

  @keyframes slideDown {
    from {
      opacity: 0;
      transform: translateY(-8px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  @media (max-width: 768px) {
    .hero {
      padding: 60px 20px 80px;
    }

    .headline {
      font-size: 2.5rem;
    }

    .subheadline {
      font-size: 1rem;
    }

    .form-row {
      flex-direction: column;
    }

    .cta-button {
      width: 100%;
    }

    .faq h2 {
      font-size: 2rem;
    }

    .faq-subtitle {
      font-size: 1rem;
    }

    .desktop-only {
      display: none;
    }
  }
</style>
