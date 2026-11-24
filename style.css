// script.js - Vanilla JS: Scroll Progress, Mobile Nav Drawer, Staggered Reveal (60fps), 3D Tilt Card & Interactive Form

document.addEventListener('DOMContentLoaded', () => {
  // 1. Scroll Progress Bar Indicator
  const progressBar = document.getElementById('scroll-progress-bar');
  const updateScrollProgress = () => {
    if (!progressBar) return;
    const scrollTop = window.scrollY || document.documentElement.scrollTop;
    const docHeight = document.documentElement.scrollHeight - document.documentElement.clientHeight;
    const scrollPercent = docHeight > 0 ? (scrollTop / docHeight) * 100 : 0;
    progressBar.style.width = `${Math.min(100, Math.max(0, scrollPercent))}%`;
  };

  window.addEventListener('scroll', updateScrollProgress, { passive: true });
  updateScrollProgress();

  // 2. Mobile Navigation Toggle with Smooth Drawer Animation
  const mobileMenuBtn = document.getElementById('mobile-menu-btn');
  const mobileMenu = document.getElementById('mobile-menu');
  const mobileLinks = document.querySelectorAll('.mobile-nav-link');

  if (mobileMenuBtn && mobileMenu) {
    const toggleMobileMenu = (open) => {
      const willOpen = open !== undefined ? open : mobileMenu.classList.contains('hidden');
      if (willOpen) {
        mobileMenu.classList.remove('hidden');
        requestAnimationFrame(() => {
          mobileMenu.classList.add('open');
          mobileMenuBtn.setAttribute('aria-expanded', 'true');
        });
      } else {
        mobileMenu.classList.remove('open');
        mobileMenuBtn.setAttribute('aria-expanded', 'false');
        setTimeout(() => {
          if (!mobileMenu.classList.contains('open')) {
            mobileMenu.classList.add('hidden');
          }
        }, 250);
      }
    };

    mobileMenuBtn.addEventListener('click', () => {
      toggleMobileMenu();
    });

    mobileLinks.forEach(link => {
      link.addEventListener('click', () => {
        toggleMobileMenu(false);
      });
    });

    // Close menu when clicking outside
    document.addEventListener('click', (e) => {
      if (!mobileMenu.classList.contains('hidden') && 
          !mobileMenu.contains(e.target) && 
          !mobileMenuBtn.contains(e.target)) {
        toggleMobileMenu(false);
      }
    });
  }

  // 3. Smooth Scroll Spy / Pill Navbar Dynamic Border & Compact State
  const navbar = document.getElementById('navbar');
  window.addEventListener('scroll', () => {
    if (window.scrollY > 30) {
      navbar.classList.add('shadow-2xl');
      navbar.style.backgroundColor = 'rgba(255, 255, 255, 0.08)';
      navbar.style.borderColor = 'rgba(255, 255, 255, 0.28)';
      navbar.style.paddingTop = '0.65rem';
      navbar.style.paddingBottom = '0.65rem';
    } else {
      navbar.classList.remove('shadow-2xl');
      navbar.style.backgroundColor = 'rgba(255, 255, 255, 0.05)';
      navbar.style.borderColor = 'rgba(255, 255, 255, 0.18)';
      navbar.style.paddingTop = '0.75rem';
      navbar.style.paddingBottom = '0.75rem';
    }
  }, { passive: true });

  // 4. 60fps Staggered Scroll Reveal Observer
  const revealElements = document.querySelectorAll('.reveal-on-scroll');
  if ('IntersectionObserver' in window) {
    const revealObserver = new IntersectionObserver((entries, observer) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) {
          entry.target.classList.add('revealed');
          observer.unobserve(entry.target);
        }
      });
    }, {
      root: null,
      threshold: 0.08,
      rootMargin: '0px 0px -25px 0px'
    });

    revealElements.forEach(el => revealObserver.observe(el));
  } else {
    revealElements.forEach(el => el.classList.add('revealed'));
  }

  // 5. Subtle 3D Tilt Effect on Hero Card (Mouse / Pointer only, disabled on touch/reduced-motion)
  const tiltContainer = document.querySelector('.tilt-card-container');
  const tiltCard = document.querySelector('.tilt-card');

  if (tiltContainer && tiltCard && window.matchMedia('(hover: hover) and (pointer: fine)').matches) {
    const prefersReducedMotion = window.matchMedia('(prefers-reduced-motion: reduce)').matches;

    if (!prefersReducedMotion) {
      let isHovering = false;

      tiltContainer.addEventListener('mouseenter', () => {
        isHovering = true;
      });

      tiltContainer.addEventListener('mousemove', (e) => {
        if (!isHovering) return;
        const rect = tiltContainer.getBoundingClientRect();
        const x = e.clientX - rect.left;
        const y = e.clientY - rect.top;

        const centerX = rect.width / 2;
        const centerY = rect.height / 2;

        // Subtle tilt: max ±6 degrees for elegant professional polish
        const rotateX = ((centerY - y) / centerY) * 6;
        const rotateY = ((x - centerX) / centerX) * 6;

        tiltCard.style.transform = `rotateX(${rotateX.toFixed(2)}deg) rotateY(${rotateY.toFixed(2)}deg) translateY(-4px)`;
      });

      tiltContainer.addEventListener('mouseleave', () => {
        isHovering = false;
        tiltCard.style.transform = 'rotateX(0deg) rotateY(0deg) translateY(0)';
      });
    }
  }

  // 6. Smooth scroll handler for anchor links
  document.querySelectorAll('a[href^="#"]').forEach(anchor => {
    anchor.addEventListener('click', function (e) {
      const targetId = this.getAttribute('href');
      if (targetId === '#') return;
      const targetEl = document.querySelector(targetId);
      if (targetEl) {
        e.preventDefault();
        targetEl.scrollIntoView({
          behavior: 'smooth',
          block: 'start'
        });
      }
    });
  });

  // 7. KostAdvisor Consultation Form Handling with Animated State Feedback
  const advisorForm = document.getElementById('advisor-form');
  const formStatus = document.getElementById('form-status');
  const submitBtn = document.getElementById('submit-btn');

  if (advisorForm) {
    advisorForm.addEventListener('submit', (e) => {
      e.preventDefault();

      const name = document.getElementById('user-name').value.trim();
      const whatsapp = document.getElementById('user-wa').value.trim();
      const campus = document.getElementById('user-campus').value;
      const budget = document.getElementById('user-budget').value;

      if (!name || !whatsapp || !campus || !budget) {
        showStatus('Harap isi semua kolom wajib bertanda bintang (*).', 'error');
        return;
      }

      // Collect selected preferences checkboxes
      const selectedPrefs = Array.from(document.querySelectorAll('input[name="preferences"]:checked')).map(cb => cb.value);

      // Loading state with spinner
      submitBtn.disabled = true;
      const originalText = submitBtn.innerHTML;
      submitBtn.innerHTML = `
        <svg class="animate-spin -ml-1 mr-2 h-4 w-4 text-white inline-block" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
          <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
          <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
        </svg>
        Menghubungkan ke KostAdvisor...
      `;

      setTimeout(() => {
        submitBtn.disabled = false;
        submitBtn.innerHTML = originalText;
        showStatus(
          `Halo <strong>${name}</strong>! Preferensi kos untuk area <strong>${campus}</strong> telah diterima. Rekomendasi kos bebas banjir & bergaransi Rekber Escrow sedang dikirim ke WhatsApp <strong>${whatsapp}</strong> oleh tim kurator kami.`,
          'success'
        );
        advisorForm.reset();
      }, 900);
    });
  }

  function showStatus(message, type) {
    if (!formStatus) return;
    formStatus.classList.remove('hidden', 'border-sky-500', 'text-sky-200', 'border-rose-500', 'text-rose-200', 'form-status-animate');

    // Force animation reflow
    void formStatus.offsetWidth;
    formStatus.classList.add('form-status-animate');

    if (type === 'success') {
      formStatus.classList.add('border', 'border-sky-500/50', 'text-sky-200');
      formStatus.style.backgroundColor = 'rgba(2, 132, 199, 0.08)';
      formStatus.innerHTML = `
        <div class="flex items-start gap-3">
          <svg class="w-5 h-5 text-sky-400 shrink-0 mt-0.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
          <div class="text-sm leading-relaxed">${message}</div>
        </div>
      `;
    } else {
      formStatus.classList.add('border', 'border-rose-500/50', 'text-rose-200');
      formStatus.style.backgroundColor = 'rgba(244, 63, 94, 0.08)';
      formStatus.innerHTML = `
        <div class="flex items-start gap-3">
          <svg class="w-5 h-5 text-rose-400 shrink-0 mt-0.5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4m0 4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
          <div class="text-sm leading-relaxed">${message}</div>
        </div>
      `;
    }

    formStatus.scrollIntoView({ behavior: 'smooth', block: 'nearest' });
  }
});
