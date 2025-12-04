<script lang="ts">
  const shareUrl = window.location.origin;
  const shareText =
    "I just joined the MiseEnCode waitlist! Get fully scoped project kits delivered monthly—design files, assets, and requirements included. Skip the planning, start coding!";

  let copied = false;

  function copyLink() {
    navigator.clipboard.writeText(shareUrl);
    copied = true;
    setTimeout(() => {
      copied = false;
    }, 2000);
  }

  function shareOnFacebook() {
    const url = `https://www.facebook.com/sharer/sharer.php?u=${encodeURIComponent(shareUrl)}`;
    window.open(url, "_blank", "width=600,height=400");
  }

  function shareOnX() {
    const url = `https://twitter.com/intent/tweet?text=${encodeURIComponent(shareText)}&url=${encodeURIComponent(shareUrl)}`;
    window.open(url, "_blank", "width=600,height=400");
  }

  function shareOnWhatsApp() {
    const url = `https://wa.me/?text=${encodeURIComponent(shareText + " " + shareUrl)}`;
    window.open(url, "_blank");
  }
</script>

<div class="thanks-page">
  <div class="container">
    <div class="logo-icon">
      <svg viewBox="0 0 24 24" fill="currentColor">
        <path d="M3 3h8v8H3V3zm10 0h8v8h-8V3zM3 13h8v8H3v-8zm10 0h8v8h-8v-8z" />
      </svg>
    </div>

    <h1>You're on the waitlist</h1>
    <p class="message">
      You've successfully secured your spot. Excited?<br />
      Feel free to refer to your friends!
    </p>

    <div class="link-section">
      <input type="text" readonly value={shareUrl} class="link-input" />
      <button class="copy-btn" on:click={copyLink}>
        {#if copied}
          <svg
            viewBox="0 0 24 24"
            width="20"
            height="20"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
          >
            <polyline points="20 6 9 17 4 12"></polyline>
          </svg>
        {:else}
          <svg
            viewBox="0 0 24 24"
            width="20"
            height="20"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
          >
            <rect x="9" y="9" width="13" height="13" rx="2" ry="2"></rect>
            <path d="M5 15H4a2 2 0 0 1-2-2V4a2 2 0 0 1 2-2h9a2 2 0 0 1 2 2v1"
            ></path>
          </svg>
        {/if}
      </button>
    </div>

    <div class="divider">
      <span>or</span>
    </div>

    <div class="share-buttons">
      <button class="share-btn x-btn" on:click={shareOnX} title="Share on X">
        <svg viewBox="0 0 24 24" width="20" height="20" fill="currentColor">
          <path
            d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"
          />
        </svg>
      </button>

      <button
        class="share-btn whatsapp-btn"
        on:click={shareOnWhatsApp}
        title="Share on WhatsApp"
      >
        <svg viewBox="0 0 24 24" width="20" height="20" fill="currentColor">
          <path
            d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"
          />
        </svg>
      </button>

      <button
        class="share-btn facebook-btn"
        on:click={shareOnFacebook}
        title="Share on Facebook"
      >
        <svg viewBox="0 0 24 24" width="20" height="20" fill="currentColor">
          <path
            d="M24 12.073c0-6.627-5.373-12-12-12s-12 5.373-12 12c0 5.99 4.388 10.954 10.125 11.854v-8.385H7.078v-3.47h3.047V9.43c0-3.007 1.792-4.669 4.533-4.669 1.312 0 2.686.235 2.686.235v2.953H15.83c-1.491 0-1.956.925-1.956 1.874v2.25h3.328l-.532 3.47h-2.796v8.385C19.612 23.027 24 18.062 24 12.073z"
          />
        </svg>
      </button>
    </div>
  </div>
</div>

<style>
  .thanks-page {
    min-height: 100vh;
    background: #fafafa;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 40px 20px;
  }

  .container {
    max-width: 500px;
    width: 100%;
    text-align: center;
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

  h1 {
    font-size: 2.5rem;
    margin: 0 0 16px;
    color: #111827;
    font-weight: 500;
  }

  .message {
    font-size: 1rem;
    color: #6b7280;
    line-height: 1.6;
    margin: 0 0 40px;
  }

  .link-section {
    display: flex;
    gap: 8px;
    margin-bottom: 32px;
    background: white;
    border: 1px solid #e5e7eb;
    border-radius: 8px;
    padding: 4px;
  }

  .link-input {
    flex: 1;
    padding: 12px 16px;
    border: none;
    background: transparent;
    font-size: 0.875rem;
    color: #6b7280;
    font-family: "DM Sans", sans-serif;
  }

  .link-input:focus {
    outline: none;
  }

  .copy-btn {
    padding: 10px 16px;
    background: white;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    transition: all 0.2s ease;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #6b7280;
  }

  .copy-btn:hover {
    background: #f9fafb;
    color: #111827;
  }

  .divider {
    position: relative;
    text-align: center;
    margin: 32px 0;
  }

  .divider::before {
    content: "";
    position: absolute;
    top: 50%;
    left: 0;
    right: 0;
    height: 1px;
    background: #e5e7eb;
  }

  .divider span {
    position: relative;
    background: #fafafa;
    padding: 0 16px;
    color: #9ca3af;
    font-size: 0.875rem;
  }

  .share-buttons {
    display: flex;
    gap: 12px;
    justify-content: center;
  }

  .share-btn {
    width: 48px;
    height: 48px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.2s ease;
    display: flex;
    align-items: center;
    justify-content: center;
    background: white;
    border: 1px solid #e5e7eb;
  }

  .share-btn:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  }

  .share-btn:active {
    transform: translateY(0);
  }

  .x-btn {
    color: #000000;
  }

  .x-btn:hover {
    background: #000000;
    color: white;
    border-color: #000000;
  }

  .whatsapp-btn {
    color: #25d366;
  }

  .whatsapp-btn:hover {
    background: #25d366;
    color: white;
    border-color: #25d366;
  }

  .facebook-btn {
    color: #1877f2;
  }

  .facebook-btn:hover {
    background: #1877f2;
    color: white;
    border-color: #1877f2;
  }

  @media (max-width: 768px) {
    h1 {
      font-size: 2rem;
    }

    .message {
      font-size: 0.95rem;
    }

    .link-input {
      font-size: 0.8rem;
    }
  }
</style>
