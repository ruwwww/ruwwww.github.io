---
layout: page
title: gallery
permalink: /gallery/
nav: true
nav_order: 4
description: Digital artwork, fanart, and character visual studies
---

<style>
  #gallery-container.blurred {
    filter: blur(14px);
    pointer-events: none;
    user-select: none;
    transition: filter 0.35s ease;
  }
  .warning-modal-box {
    background-color: var(--global-bg-color) !important;
    color: var(--global-text-color) !important;
    border: 1px solid var(--global-divider-color) !important;
    border-radius: 12px;
  }
  .art-card {
    background-color: var(--global-card-bg-color, var(--global-bg-color));
    border: 1px solid var(--global-divider-color);
    border-radius: 8px;
    overflow: hidden;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
  }
  .art-card:hover {
    transform: translateY(-3px);
    box-shadow: 0 6px 18px rgba(0,0,0,0.12);
  }
  .art-card figcaption {
    margin: 0;
    padding: 0.75rem 1rem 1rem;
  }
</style>

<!-- Warning Modal (Bootstrap 4) -->
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
<div id="gallery-container" class="blurred mt-4">
  <div class="row">
    <!-- Artwork 1: Burstinatrix -->
    <div class="col-12 col-md-6 mb-4">
      <div class="art-card h-100">
        {% include figure.liquid loading="eager" path="assets/img/art/burstinatrix.png" title="Elemental HERO Burstinatrix" class="img-fluid w-100" zoomable=true %}
        <div class="p-3 text-center">
          <h5 class="font-weight-bold mb-1">Elemental HERO Burstinatrix</h5>
          <p class="text-muted small mb-0">Yu-Gi-Oh! GX · Character & Form Study</p>
        </div>
      </div>
    </div>

    <!-- Artwork 2: Supergirl -->
    <div class="col-12 col-md-6 mb-4">
      <div class="art-card h-100">
        {% include figure.liquid loading="eager" path="assets/img/art/supergirl.png" title="Supergirl in the Rain" class="img-fluid w-100" zoomable=true %}
        <div class="p-3 text-center">
          <h5 class="font-weight-bold mb-1">Supergirl</h5>
          <p class="text-muted small mb-0">DC Comics · Wet Surface & Atmospheric Lighting</p>
        </div>
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
    document.getElementById('gallery-container').classList.remove('blurred');
  }

  function declineWarning() {
    window.location.href = "{{ '/' | relative_url }}";
  }

  function checkConsent() {
    if (sessionStorage.getItem('gallery_consent') === 'granted') {
      var container = document.getElementById('gallery-container');
      if (container) container.classList.remove('blurred');
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
