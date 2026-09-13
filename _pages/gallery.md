---
layout: page
title: gallery
permalink: /gallery/
nav: true
nav_order: 4
description: Digital artwork, fanart, and character visual studies
images:
  spotlight: true
---

<style>
  /* Gallery Grid & Card */
  .art-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 1.5rem;
    margin-top: 1.5rem;
  }
  .art-card {
    background-color: var(--global-card-bg-color, var(--global-bg-color));
    border: 1px solid var(--global-divider-color);
    border-radius: 12px;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
  }
  .art-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 8px 24px rgba(0, 0, 0, 0.15);
  }
  .art-thumb-link {
    display: block;
    position: relative;
    width: 100%;
    aspect-ratio: 3 / 4;
    overflow: hidden;
    background-color: rgba(0, 0, 0, 0.05);
    cursor: zoom-in;
  }
  .art-thumb-link img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    object-position: top center;
    transition: transform 0.35s ease;
    display: block;
  }
  .art-thumb-link:hover img {
    transform: scale(1.04);
  }
  .art-thumb-overlay {
    position: absolute;
    inset: 0;
    background: rgba(0, 0, 0, 0.25);
    opacity: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #ffffff;
    font-size: 1.5rem;
    transition: opacity 0.25s ease;
  }
  .art-thumb-link:hover .art-thumb-overlay {
    opacity: 1;
  }
  .art-info {
    padding: 1rem;
    text-align: center;
  }
  .art-info h5 {
    font-size: 1.05rem;
    font-weight: 700;
    margin-bottom: 0.25rem;
  }
  .art-info p {
    font-size: 0.85rem;
    color: var(--global-text-color-light, #888);
    margin: 0;
  }

  /* Warning Blur state */
  #gallery-container.is-blurred {
    filter: blur(16px);
    pointer-events: none;
    user-select: none;
  }
  .warning-modal-box {
    background-color: var(--global-bg-color) !important;
    color: var(--global-text-color) !important;
    border: 1px solid var(--global-divider-color) !important;
    border-radius: 12px;
  }
</style>

<!-- Content Warning Modal (Bootstrap 4) -->
<div class="modal fade" id="galleryWarningModal" tabindex="-1" role="dialog" data-backdrop="static" data-keyboard="false" aria-hidden="true">
  <div class="modal-dialog modal-dialog-centered" role="document">
    <div class="modal-content warning-modal-box p-4 text-center shadow-lg">
      <div class="modal-body">
        <div class="mb-3">
          <i class="fa-solid fa-triangle-exclamation fa-3x text-warning"></i>
        </div>
        <h4 class="font-weight-bold mb-2">Content Warning & Disclaimer</h4>
        <p class="text-muted small mb-4">
          Galeri ini memuat karya ilustrasi digital, fanart karakter, dan studi visual stylize.<br>
          Beberapa karya mungkin memuat desain kostum ketat atau tema visual figuratif.
        </p>
        <div class="d-flex justify-content-center gap-3">
          <button type="button" class="btn btn-sm btn-outline-secondary mr-2" onclick="declineWarning()">
            <i class="fa-solid fa-arrow-left mr-1"></i> Kembali
          </button>
          <button type="button" class="btn btn-sm btn-primary" onclick="acceptWarning()">
            Saya Mengerti & Lanjutkan <i class="fa-solid fa-arrow-right ml-1"></i>
          </button>
        </div>
      </div>
    </div>
  </div>
</div>

<!-- Gallery Container -->
<div id="gallery-container" class="is-blurred">
  <div class="art-grid">
    <!-- Artwork 1: Burstinatrix -->
    <div class="art-card">
      <a class="spotlight art-thumb-link"
         href="{{ '/assets/img/art/burstinatrix.png' | relative_url }}"
         data-title="Elemental HERO Burstinatrix"
         data-description="Yu-Gi-Oh! GX · Character & Form Study">
        <img src="{{ '/assets/img/art/burstinatrix.png' | relative_url }}"
             alt="Elemental HERO Burstinatrix"
             loading="eager">
        <div class="art-thumb-overlay">
          <i class="fa-solid fa-expand"></i>
        </div>
      </a>
      <div class="art-info">
        <h5>Elemental HERO Burstinatrix</h5>
        <p>Yu-Gi-Oh! GX · Character & Form Study</p>
      </div>
    </div>

    <!-- Artwork 2: Supergirl -->
    <div class="art-card">
      <a class="spotlight art-thumb-link"
         href="{{ '/assets/img/art/supergirl.png' | relative_url }}"
         data-title="Supergirl in the Rain"
         data-description="DC Comics · Wet Surface & Atmospheric Lighting">
        <img src="{{ '/assets/img/art/supergirl.png' | relative_url }}"
             alt="Supergirl in the Rain"
             loading="eager">
        <div class="art-thumb-overlay">
          <i class="fa-solid fa-expand"></i>
        </div>
      </a>
      <div class="art-info">
        <h5>Supergirl</h5>
        <p>DC Comics · Wet Surface & Atmospheric Lighting</p>
      </div>
    </div>
  </div>
</div>

<script>
  function showModal() {
    $('#galleryWarningModal').modal({
      backdrop: 'static',
      keyboard: false,
      show: true
    });
  }

  function acceptWarning() {
    sessionStorage.setItem('gallery_consent', 'granted');
    $('#galleryWarningModal').modal('hide');
    var container = document.getElementById('gallery-container');
    if (container) {
      container.classList.remove('is-blurred');
    }
  }

  function declineWarning() {
    window.location.href = "{{ '/' | relative_url }}";
  }

  function checkConsent() {
    if (sessionStorage.getItem('gallery_consent') === 'granted') {
      var container = document.getElementById('gallery-container');
      if (container) {
        container.classList.remove('is-blurred');
      }
    } else {
      showModal();
    }
  }

  if (document.readyState === 'loading') {
    document.addEventListener('DOMContentLoaded', checkConsent);
  } else {
    checkConsent();
  }
</script>
