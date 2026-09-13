---
layout: page
title: gallery
permalink: /gallery/
nav: true
nav_order: 4
images:
  spotlight: true
---

<style>
  /* Pure Visual Masonry */
  .gallery-masonry {
    column-count: 2;
    column-gap: 1.5rem;
    margin-top: 2rem;
  }
  @media (max-width: 600px) {
    .gallery-masonry {
      column-count: 1;
      column-gap: 0;
    }
  }

  .gallery-item {
    break-inside: avoid;
    margin-bottom: 1.5rem;
    border-radius: 12px;
    overflow: hidden;
    background-color: var(--global-card-bg-color, var(--global-bg-color));
    box-shadow: 0 4px 18px rgba(0, 0, 0, 0.12);
    transition: transform 0.25s ease, box-shadow 0.25s ease;
    position: relative;
  }

  .gallery-item:hover {
    transform: translateY(-4px);
    box-shadow: 0 10px 28px rgba(0, 0, 0, 0.22);
  }

  .gallery-link {
    display: block;
    width: 100%;
    cursor: zoom-in;
    position: relative;
    overflow: hidden;
  }

  .gallery-link img {
    width: 100%;
    height: auto;
    display: block;
    transition: transform 0.35s ease, filter 0.35s ease;
  }

  .gallery-link:hover img {
    transform: scale(1.02);
  }

  /* Warning Modal & Blur state */
  #gallery-container.is-blurred {
    filter: blur(16px);
    pointer-events: none;
    user-select: none;
  }

  .warning-modal-box {
    background-color: var(--global-bg-color) !important;
    color: var(--global-text-color) !important;
    border: 1px solid var(--global-divider-color) !important;
    border-radius: 14px;
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
          Galeri ini memuat karya ilustrasi visual digital dan fanart karakter.<br>
          Beberapa karya mungkin memuat kostum ketat atau tema visual figuratif.
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

<!-- Pure Visual Gallery -->
<div id="gallery-container" class="is-blurred">
  <div class="gallery-masonry">
    <!-- Item 1: Burstinatrix -->
    <div class="gallery-item">
      <a class="spotlight gallery-link"
         href="{{ '/assets/img/art/burstinatrix.png' | relative_url }}">
        <img src="{{ '/assets/img/art/burstinatrix.png' | relative_url }}"
             alt="Visual artwork"
             loading="eager">
      </a>
    </div>

    <!-- Item 2: Supergirl -->
    <div class="gallery-item">
      <a class="spotlight gallery-link"
         href="{{ '/assets/img/art/supergirl.png' | relative_url }}">
        <img src="{{ '/assets/img/art/supergirl.png' | relative_url }}"
             alt="Visual artwork"
             loading="eager">
      </a>
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
