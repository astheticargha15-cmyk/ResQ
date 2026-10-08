<!DOCTYPE html>
<html lang="en" data-theme="dark">
<head>
<meta charset="UTF-8">

<meta name="viewport"
      content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

<meta name="theme-color" content="#0f172a">

<title>ResQ — Emergency Safety App</title>

<!-- Font -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@400;500;600;700;800&display=swap" rel="stylesheet">

<!-- Font Awesome -->
<link rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">

<style>

/* ==========================================================
   RESQ — SINGLE FILE CSS
   ========================================================== */

:root {
    --bg-primary: #0f172a;
    --bg-card: rgba(30, 41, 59, 0.75);
    --border-card: rgba(255, 255, 255, 0.1);
    --text-main: #f8fafc;
    --text-sub: #94a3b8;
    --accent-red: #ef4444;
    --accent-red-hover: #dc2626;
    --accent-blue: #3b82f6;
    --accent-green: #10b981;
    --accent-yellow: #f59e0b;
    --shadow-glow: rgba(239, 68, 68, 0.35);
}

[data-theme="light"] {
    --bg-primary: #f1f5f9;
    --bg-card: rgba(255, 255, 255, 0.92);
    --border-card: rgba(0, 0, 0, 0.08);
    --text-main: #0f172a;
    --text-sub: #64748b;
    --shadow-glow: rgba(239, 68, 68, 0.2);
}

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
    font-family: 'Plus Jakarta Sans', sans-serif;
    -webkit-tap-highlight-color: transparent;
    transition:
        background-color 0.25s ease,
        color 0.25s ease,
        border-color 0.25s ease;
}

html {
    min-height: 100%;
}

body {
    background: var(--bg-primary);
    color: var(--text-main);
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: flex-start;
    padding: 12px;
    padding-bottom: 90px;
}

button,
input,
select {
    font: inherit;
}

button {
    -webkit-user-select: none;
    user-select: none;
}

.app-container {
    width: 100%;
    max-width: 440px;
    display: flex;
    flex-direction: column;
    gap: 16px;
}

/* ==========================================================
   SPLASH
   ========================================================== */

.splash-screen {
    position: fixed;
    inset: 0;
    width: 100vw;
    height: 100vh;
    background: #090d16;
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 9999;
    opacity: 1;
    visibility: visible;
    transition: opacity .5s ease, visibility .5s ease;
}

.splash-screen.hidden {
    opacity: 0;
    visibility: hidden;
    pointer-events: none;
}

.splash-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    gap: 12px;
}

.splash-shield {
    position: relative;
    width: 80px;
    height: 80px;
    background: var(--accent-red);
    border-radius: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #fff;
    font-size: 38px;
    animation: scaleIn .8s cubic-bezier(.175,.885,.32,1.275) forwards;
}

.splash-ripple {
    position: absolute;
    width: 100%;
    height: 100%;
    border-radius: 20px;
    border: 2px solid var(--accent-red);
    animation: rippleEffect 1.8s infinite ease-out;
}

.splash-title {
    font-size: 28px;
    font-weight: 800;
    color: #fff;
    letter-spacing: -.5px;
    animation: fadeIn .6s ease .3s forwards;
    opacity: 0;
}

.splash-tagline {
    font-size: 13px;
    color: #94a3b8;
    animation: fadeIn .6s ease .5s forwards;
    opacity: 0;
}

.splash-author {
    font-size: 11px;
    color: #64748b;
    margin-top: 10px;
    letter-spacing: 1px;
    text-transform: uppercase;
    animation: fadeIn .6s ease .7s forwards;
    opacity: 0;
}

@keyframes scaleIn {
    0% {
        transform: scale(0);
        opacity: 0;
    }
    100% {
        transform: scale(1);
        opacity: 1;
    }
}

@keyframes rippleEffect {
    0% {
        transform: scale(1);
        opacity: .8;
    }
    100% {
        transform: scale(1.6);
        opacity: 0;
    }
}

@keyframes fadeIn {
    to {
        opacity: 1;
    }
}

/* ==========================================================
   HEADER
   ========================================================== */

.app-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 8px 4px;
}

.brand {
    display: flex;
    align-items: center;
    gap: 10px;
}

.brand-icon {
    width: 36px;
    height: 36px;
    background: var(--accent-red);
    border-radius: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #fff;
    font-size: 18px;
    box-shadow: 0 4px 12px var(--shadow-glow);
}

.brand-text h1 {
    font-size: 18px;
    font-weight: 800;
    line-height: 1.1;
}

.brand-subtitle {
    font-size: 11px;
    color: var(--text-sub);
}

.header-actions {
    display: flex;
    gap: 8px;
}

.icon-btn {
    width: 36px;
    height: 36px;
    border-radius: 50%;
    background: var(--bg-card);
    border: 1px solid var(--border-card);
    color: var(--text-main);
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    font-size: 14px;
}

/* ==========================================================
   VIEWS
   ========================================================== */

.view-section {
    display: none;
    flex-direction: column;
    gap: 16px;
    animation: fadeInView .3s ease;
}

.view-section.active {
    display: flex;
}

@keyframes fadeInView {
    from {
        opacity: 0;
        transform: translateY(4px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

/* ==========================================================
   CARDS
   ========================================================== */

.glass-card {
    background: var(--bg-card);
    border: 1px solid var(--border-card);
    border-radius: 18px;
    padding: 18px;
    backdrop-filter: blur(12px);
    box-shadow: 0 8px 24px rgba(0,0,0,.08);
}

.banner-card {
    padding: 4px 6px;
}

.banner-card p {
    font-size: 13px;
    color: var(--text-sub);
    font-weight: 500;
}

/* ==========================================================
   SOS
   ========================================================== */

.sos-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    padding: 24px 16px;
    position: relative;
    overflow: hidden;
}

.sos-wrapper {
    position: relative;
    margin: 10px 0 16px;
}

.sos-ring {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
    width: 156px;
    height: 156px;
    border-radius: 50%;
    background: var(--accent-red);
    opacity: .25;
    animation: sosRingPulse 2s infinite ease-in-out;
}

@keyframes sosRingPulse {
    0% {
        transform: translate(-50%,-50%) scale(.9);
        opacity: .5;
    }
    50% {
        transform: translate(-50%,-50%) scale(1.2);
        opacity: 0;
    }
    100% {
        transform: translate(-50%,-50%) scale(.9);
        opacity: 0;
    }
}

.sos-main-btn {
    position: relative;
    z-index: 2;
    width: 136px;
    height: 136px;
    border-radius: 50%;
    background: linear-gradient(135deg,#f87171,#dc2626);
    border: 4px solid rgba(255,255,255,.25);
    color: #fff;
    font-size: 26px;
    font-weight: 800;
    cursor: pointer;
    box-shadow: 0 10px 25px var(--shadow-glow);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 2px;
    outline: none;
    user-select: none;
    touch-action: none;
}

.sos-main-btn:active {
    transform: scale(.96);
}

.sos-main-btn span {
    font-size: 24px;
    line-height: 1;
}

.sos-main-btn small {
    font-size: 10px;
    font-weight: 600;
    letter-spacing: .5px;
    opacity: .85;
    text-transform: uppercase;
}

.sos-progress-bar {
    width: 100%;
    max-width: 220px;
    height: 4px;
    background: rgba(255,255,255,.1);
    border-radius: 2px;
    overflow: hidden;
    margin-bottom: 12px;
}

.sos-progress-bar div {
    width: 0%;
    height: 100%;
    background: var(--accent-red);
    transition: width .1s linear;
}

.sos-instruction {
    font-size: 12px;
    color: var(--text-sub);
    line-height: 1.4;
}

/* ==========================================================
   SECTIONS
   ========================================================== */

.section-block {
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.section-title h2 {
    font-size: 14px;
    font-weight: 700;
    display: flex;
    align-items: center;
    gap: 8px;
}

.section-title h2 i {
    color: var(--accent-red);
}

.section-header-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 12px;
}

.section-header-row h3 {
    font-size: 14px;
    font-weight: 700;
    display: flex;
    align-items: center;
    gap: 8px;
}

.section-header-row h3 i {
    color: var(--accent-blue);
}

/* ==========================================================
   HELPLINES
   ========================================================== */

.helpline-grid {
    display: grid;
    grid-template-columns: repeat(2,1fr);
    gap: 10px;
}

.helpline-card {
    background: var(--bg-card);
    border: 1px solid var(--border-card);
    border-radius: 14px;
    padding: 14px 10px;
    text-align: center;
    text-decoration: none;
    color: var(--text-main);
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 4px;
    backdrop-filter: blur(10px);
}

.helpline-card.primary-helpline {
    grid-column: span 2;
    background: linear-gradient(
        135deg,
        rgba(239,68,68,.15),
        rgba(30,41,59,.8)
    );
    border-color: rgba(239,68,68,.3);
}

.helpline-card i {
    font-size: 18px;
    color: var(--accent-blue);
}

.helpline-card.primary-helpline i {
    color: var(--accent-red);
}

.helpline-card strong {
    font-size: 16px;
}

.helpline-card span {
    font-size: 11px;
    color: var(--text-sub);
}

.disclaimer-text {
    font-size: 11px;
    color: var(--text-sub);
    font-style: italic;
}

/* ==========================================================
   LOCATION
   ========================================================== */

.badge-status {
    font-size: 10px;
    font-weight: 600;
    padding: 3px 8px;
    background: rgba(59,130,246,.15);
    color: var(--accent-blue);
    border-radius: 20px;
}

.location-box {
    background: rgba(0,0,0,.15);
    border-radius: 10px;
    padding: 12px;
    font-size: 12px;
    color: var(--text-sub);
    margin-bottom: 10px;
    word-break: break-word;
}

.location-meta {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    font-size: 11px;
    color: var(--text-sub);
    margin-bottom: 12px;
    padding: 0 4px;
}

.action-grid-3 {
    display: grid;
    grid-template-columns: repeat(3,1fr);
    gap: 8px;
}

/* ==========================================================
   BUTTONS
   ========================================================== */

.btn-sm {
    padding: 9px 8px;
    border-radius: 10px;
    border: none;
    font-size: 12px;
    font-weight: 600;
    cursor: pointer;
    text-align: center;
}

.btn-blue {
    background: var(--accent-blue);
    color: #fff;
    border: none;
    padding: 10px;
    border-radius: 10px;
    cursor: pointer;
    font-weight: 600;
}

.btn-secondary {
    background: rgba(255,255,255,.1);
    color: var(--text-main);
    border: 1px solid var(--border-card);
}

.btn-secondary:disabled,
.btn-blue:disabled {
    opacity: .4;
    cursor: not-allowed;
}

.btn-green {
    background: var(--accent-green);
    color: #fff;
    border: none;
    padding: 10px 14px;
    border-radius: 10px;
    font-weight: 600;
    cursor: pointer;
}

.text-btn-danger {
    background: none;
    border: none;
    color: var(--accent-red);
    font-size: 12px;
    font-weight: 600;
    cursor: pointer;
}

/* ==========================================================
   CONTACTS
   ========================================================== */

.sub-note {
    font-size: 12px;
    color: var(--text-sub);
    margin-bottom: 14px;
}

.contact-form {
    display: flex;
    flex-direction: column;
    gap: 10px;
    margin-bottom: 16px;
}

.contact-form input[type="text"],
.contact-form input[type="tel"] {
    width: 100%;
    padding: 10px 14px;
    border-radius: 10px;
    border: 1px solid var(--border-card);
    background: rgba(0,0,0,.2);
    color: var(--text-main);
    font-size: 13px;
    outline: none;
}

.form-row-check {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 10px;
    font-size: 12px;
    color: var(--text-sub);
}

.form-row-check label {
    display: flex;
    align-items: center;
    gap: 6px;
}

.contacts-container {
    display: flex;
    flex-direction: column;
    gap: 8px;
    max-height: 280px;
    overflow-y: auto;
}

.contact-item-card {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 10px;
    padding: 10px 12px;
    background: rgba(0,0,0,.15);
    border-radius: 10px;
    border: 1px solid var(--border-card);
}

.contact-info-block {
    min-width: 0;
    display: flex;
    flex-direction: column;
    gap: 2px;
}

.contact-info-block span {
    font-size: 13px;
    font-weight: 600;
    word-break: break-word;
}

.contact-info-block small {
    font-size: 11px;
    color: var(--text-sub);
}

.badge-primary {
    font-size: 9px;
    background: rgba(16,185,129,.2);
    color: var(--accent-green);
    padding: 1px 6px;
    border-radius: 10px;
    margin-left: 6px;
}

.contact-actions {
    display: flex;
    gap: 8px;
    align-items: center;
}

.contact-actions button {
    background: none;
    border: none;
    color: var(--text-sub);
    font-size: 14px;
    cursor: pointer;
    padding: 4px;
}

.call-icon {
    color: var(--accent-green) !important;
}

.wa-icon {
    color: #25d366 !important;
}

.del-icon {
    color: var(--accent-red) !important;
}

/* ==========================================================
   FIRST AID
   ========================================================== */

.search-input {
    width: 100%;
    padding: 10px 14px;
    border-radius: 10px;
    border: 1px solid var(--border-card);
    background: rgba(0,0,0,.2);
    color: var(--text-main);
    font-size: 13px;
    margin-bottom: 12px;
    outline: none;
}

.filter-chips {
    display: flex;
    gap: 6px;
    overflow-x: auto;
    padding-bottom: 4px;
    margin-bottom: 12px;
}

.filter-chips::-webkit-scrollbar {
    display: none;
}

.chip {
    background: rgba(255,255,255,.06);
    border: 1px solid var(--border-card);
    color: var(--text-sub);
    padding: 5px 12px;
    border-radius: 20px;
    font-size: 11px;
    font-weight: 600;
    cursor: pointer;
    white-space: nowrap;
}

.chip.active {
    background: var(--accent-blue);
    color: #fff;
    border-color: var(--accent-blue);
}

.accordion-list {
    display: flex;
    flex-direction: column;
    gap: 8px;
    max-height: 320px;
    overflow-y: auto;
}

.accordion-card {
    background: rgba(0,0,0,.15);
    border-radius: 10px;
    border: 1px solid var(--border-card);
    overflow: hidden;
}

.accordion-header {
    padding: 12px;
    font-size: 13px;
    font-weight: 600;
    display: flex;
    justify-content: space-between;
    align-items: center;
    cursor: pointer;
    gap: 10px;
}

.accordion-header i {
    flex-shrink: 0;
}

.accordion-body {
    padding: 0 12px 12px;
    font-size: 12px;
    color: var(--text-sub);
    display: none;
    line-height: 1.5;
}

.accordion-card.open .accordion-body {
    display: block;
}

.aid-section-title {
    font-weight: 700;
    color: var(--text-main);
    margin-top: 6px;
    display: block;
}

.accordion-body p {
    margin-top: 3px;
}

/* ==========================================================
   SETTINGS
   ========================================================== */

.settings-card {
    display: flex;
    flex-direction: column;
    gap: 16px;
}

.settings-card h2 {
    font-size: 16px;
    display: flex;
    align-items: center;
    gap: 8px;
}

.settings-group {
    display: flex;
    flex-direction: column;
    gap: 8px;
    padding-bottom: 12px;
    border-bottom: 1px solid var(--border-card);
}

.settings-group h3 {
    font-size: 12px;
    font-weight: 700;
    text-transform: uppercase;
    color: var(--text-sub);
    letter-spacing: .5px;
}

.input-stacked {
    display: flex;
    flex-direction: column;
    gap: 4px;
}

.input-stacked label {
    font-size: 11px;
    color: var(--text-sub);
}

.input-stacked input {
    padding: 9px 12px;
    border-radius: 8px;
    border: 1px solid var(--border-card);
    background: rgba(0,0,0,.2);
    color: var(--text-main);
    font-size: 13px;
    outline: none;
}

.setting-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 10px;
    font-size: 13px;
}

.setting-row select {
    padding: 6px 10px;
    border-radius: 8px;
    border: 1px solid var(--border-card);
    background: rgba(0,0,0,.2);
    color: var(--text-main);
    font-size: 12px;
    outline: none;
}

.btn-danger-outline {
    background: none;
    border: 1px solid var(--accent-red);
    color: var(--accent-red);
    padding: 8px;
    border-radius: 8px;
    font-size: 12px;
    font-weight: 600;
    cursor: pointer;
}

.privacy-note {
    font-size: 11px;
    color: var(--text-sub);
    font-style: italic;
}

.about-group p {
    font-size: 12px;
    color: var(--text-sub);
}

.creator-sign {
    font-size: 11px;
    font-weight: 700;
    color: var(--accent-blue) !important;
}

.backend-notice {
    font-size: 10px !important;
    color: var(--accent-yellow) !important;
    margin-top: 4px;
}

/* ==========================================================
   MODAL
   ========================================================== */

.modal-overlay {
    position: fixed;
    inset: 0;
    width: 100vw;
    height: 100vh;
    background: rgba(0,0,0,.7);
    backdrop-filter: blur(5px);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 999;
    opacity: 0;
    visibility: hidden;
    transition: opacity .3s ease, visibility .3s ease;
    padding: 20px;
}

.modal-overlay.active {
    opacity: 1;
    visibility: visible;
}

.modal-card {
    width: 100%;
    max-width: 380px;
    max-height: 90vh;
    overflow-y: auto;
    background: var(--bg-primary);
    border: 1px solid var(--border-card);
    border-radius: 20px;
    padding: 22px;
    display: flex;
    flex-direction: column;
    gap: 16px;
    box-shadow: 0 15px 35px rgba(0,0,0,.3);
}

.modal-header-alert {
    display: flex;
    align-items: center;
    gap: 10px;
    color: var(--accent-red);
}

.modal-header-alert i {
    font-size: 22px;
}

.modal-header-alert h2 {
    font-size: 16px;
}

.modal-desc {
    font-size: 12px;
    color: var(--text-sub);
    line-height: 1.4;
}

.modal-checklist {
    display: flex;
    flex-direction: column;
    gap: 8px;
    background: rgba(0,0,0,.15);
    padding: 12px;
    border-radius: 12px;
}

.check-item {
    font-size: 12px;
    display: flex;
    align-items: center;
    gap: 8px;
    color: var(--text-sub);
}

.check-item.success {
    color: var(--accent-green);
}

.modal-actions {
    display: flex;
    flex-direction: column;
    gap: 8px;
}

.btn-red-solid {
    background: var(--accent-red);
    color: #fff;
    padding: 10px;
    border-radius: 10px;
    text-align: center;
    text-decoration: none;
    font-weight: 600;
    font-size: 13px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 8px;
}

/* ==========================================================
   BOTTOM NAV
   ========================================================== */

.bottom-nav {
    position: fixed;
    bottom: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 100%;
    max-width: 440px;
    background: var(--bg-card);
    border-top: 1px solid var(--border-card);
    backdrop-filter: blur(15px);
    display: flex;
    justify-content: space-around;
    padding: 10px 0;
    padding-bottom: max(10px, env(safe-area-inset-bottom));
    z-index: 100;
}

.nav-item {
    background: none;
    border: none;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 3px;
    color: var(--text-sub);
    cursor: pointer;
    font-size: 10px;
    font-weight: 600;
    outline: none;
    flex: 1;
}

.nav-item i {
    font-size: 16px;
}

.nav-item.active {
    color: var(--accent-red);
}

/* ==========================================================
   SMALL DEVICES
   ========================================================== */

@media (max-width: 350px) {
    body {
        padding-left: 8px;
        padding-right: 8px;
    }

    .glass-card {
        padding: 14px;
    }

    .sos-main-btn {
        width: 125px;
        height: 125px;
    }

    .sos-ring {
        width: 145px;
        height: 145px;
    }

    .action-grid-3 {
        grid-template-columns: 1fr;
    }
}

</style>
</head>

<body>

<!-- ==========================================================
     SPLASH
     ========================================================== -->

<div id="splashScreen" class="splash-screen">
    <div class="splash-content">

        <div class="splash-shield">
            <i class="fa-solid fa-shield-halved"></i>
            <div class="splash-ripple"></div>
        </div>

        <h1 class="splash-title">ResQ</h1>

        <p class="splash-tagline" data-i18n="splashTag">
            "Emergency. Anytime. Anywhere."
        </p>

        <span class="splash-author">
            by Pritam
        </span>

    </div>
</div>


<!-- ==========================================================
     MAIN APP
     ========================================================== -->

<div class="app-container">

    <!-- HEADER -->

    <header class="app-header">

        <div class="brand">

            <div class="brand-icon">
                <i class="fa-solid fa-shield-halved"></i>
            </div>

            <div class="brand-text">
                <h1>ResQ</h1>
                <span id="userGreetingDisplay" class="brand-subtitle">
                    Stay Safe
                </span>
            </div>

        </div>

        <div class="header-actions">

            <button class="icon-btn"
                    id="netStatusIndicator"
                    title="Network Status">

                <i class="fa-solid fa-wifi"></i>

            </button>

            <button class="icon-btn"
                    id="themeToggleBtn"
                    title="Toggle Theme">

                <i class="fa-solid fa-moon" id="themeIcon"></i>

            </button>

        </div>

    </header>


    <!-- ======================================================
         HOME
         ====================================================== -->

    <main class="view-section active" id="view-home">

        <div class="banner-card">

            <p data-i18n="dashSubtitle">
                Emergency assistance at your fingertips.
            </p>

        </div>


        <!-- SOS -->

        <div class="glass-card sos-card">

            <div class="sos-wrapper">

                <div class="sos-ring"></div>

                <button class="sos-main-btn" id="sosMainBtn">

                    <i class="fa-solid fa-bell"></i>

                    <span>SOS</span>

                    <small data-i18n="holdToActivate">
                        Hold 3s
                    </small>

                </button>

            </div>

            <div class="sos-progress-bar">
                <div id="sosProgress"></div>
            </div>

            <p class="sos-instruction"
               id="sosInstructionText"
               data-i18n="sosInstruction">

                Press and hold for 3 seconds to trigger emergency alert

            </p>

        </div>


        <!-- EMERGENCY NUMBERS -->

        <div class="section-block">

            <div class="section-title">

                <h2>
                    <i class="fa-solid fa-phone-volume"></i>

                    <span data-i18n="emergencyHelplines">
                        Emergency Helplines (India)
                    </span>

                </h2>

            </div>


            <div class="helpline-grid">

                <a href="tel:112"
                   class="helpline-card primary-helpline">

                    <i class="fa-solid fa-triangle-exclamation"></i>

                    <strong>112</strong>

                    <span>National Emergency</span>

                </a>


                <a href="tel:100"
                   class="helpline-card">

                    <i class="fa-solid fa-user-shield"></i>

                    <strong>100 / 112</strong>

                    <span>Police</span>

                </a>


                <a href="tel:108"
                   class="helpline-card">

                    <i class="fa-solid fa-truck-medical"></i>

                    <strong>108 / 102</strong>

                    <span>Ambulance</span>

                </a>


                <a href="tel:101"
                   class="helpline-card">

                    <i class="fa-solid fa-fire-extinguisher"></i>

                    <strong>101</strong>

                    <span>Fire Services</span>

                </a>

            </div>


            <p class="disclaimer-text"
               data-i18n="helplineDisclaimer">

                Emergency numbers may vary by location.
                Verify local services before relying on them.

            </p>

        </div>


        <!-- LIVE LOCATION -->

        <div class="glass-card">

            <div class="section-header-row">

                <h3>
                    <i class="fa-solid fa-location-crosshairs"></i>

                    <span data-i18n="liveLocationTitle">
                        Live Location
                    </span>
                </h3>

                <span class="badge-status"
                      id="gpsStatusBadge"
                      data-i18n="gpsStandby">

                    Standby

                </span>

            </div>


            <div class="location-box"
                 id="locationStatusBox">

                <p data-i18n="locFetchPrompt">
                    Click refresh to acquire precise GPS coordinates.
                </p>

            </div>


            <div class="location-meta"
                 id="locationMetaInfo"
                 style="display:none;">

                <span id="locLatLon">
                    Lat: 0.00, Lon: 0.00
                </span>

                <span id="locAccuracy">
                    Accuracy: --
                </span>

                <span id="locTime">
                    Updated: --
                </span>

            </div>


            <div class="action-grid-3">

                <button class="btn-sm btn-blue"
                        id="refreshLocationBtn"
                        data-i18n="btnRefresh">

                    Refresh

                </button>

                <button class="btn-sm btn-secondary"
                        id="mapOpenBtn"
                        disabled
                        data-i18n="btnMaps">

                    Maps

                </button>

                <button class="btn-sm btn-secondary"
                        id="shareLocBtn"
                        disabled
                        data-i18n="btnShare">

                    Share

                </button>

            </div>

        </div>

    </main>


    <!-- ======================================================
         CONTACTS
         ====================================================== -->

    <main class="view-section" id="view-contacts">

        <div class="glass-card">

            <div class="section-header-row">

                <h2>
                    <i class="fa-solid fa-users"></i>

                    <span data-i18n="trustedContactsTitle">
                        Trusted Contacts
                    </span>
                </h2>

                <button class="text-btn-danger"
                        id="clearContactsBtn"
                        data-i18n="clearAll">

                    Clear All

                </button>

            </div>


            <p class="sub-note"
               data-i18n="storageNote">

                Your contacts are stored locally on this device via LocalStorage.

            </p>


            <form id="contactForm" class="contact-form">

                <input type="text"
                       id="cName"
                       placeholder="Contact Name"
                       maxlength="50"
                       required>

                <input type="tel"
                       id="cPhone"
                       placeholder="10-digit Mobile No."
                       inputmode="numeric"
                       maxlength="10"
                       pattern="[0-9]{10}"
                       required>

                <div class="form-row-check">

                    <label>

                        <input type="checkbox" id="cPrimary">

                        <span data-i18n="setPrimary">
                            Set as Primary
                        </span>

                    </label>

                    <button type="submit"
                            class="btn-green"
                            data-i18n="btnAdd">

                        Add Contact

                    </button>

                </div>

            </form>


            <div class="contacts-container"
                 id="contactsListContainer">

            </div>

        </div>

    </main>


    <!-- ======================================================
         FIRST AID
         ====================================================== -->

    <main class="view-section" id="view-firstaid">

        <div class="glass-card">

            <div class="section-title">

                <h2>
                    <i class="fa-solid fa-kit-medical"></i>

                    <span data-i18n="firstAidTitle">
                        First Aid Emergency Guide
                    </span>
                </h2>

            </div>


            <input type="text"
                   class="search-input"
                   id="firstAidSearch"
                   placeholder="Search condition (e.g. Bleeding, Burns)...">


            <div class="filter-chips">

                <button class="chip active"
                        data-category="all"
                        data-i18n="chipAll">

                    All

                </button>

                <button class="chip"
                        data-category="bleeding"
                        data-i18n="chipBleeding">

                    Bleeding

                </button>

                <button class="chip"
                        data-category="burns"
                        data-i18n="chipBurns">

                    Burns

                </button>

                <button class="chip"
                        data-category="poison"
                        data-i18n="chipBite">

                    Snake Bite

                </button>

                <button class="chip"
                        data-category="faint"
                        data-i18n="chipFaint">

                    Fainting

                </button>

            </div>


            <div class="accordion-list"
                 id="firstAidAccordion">

            </div>

        </div>

    </main>


    <!-- ======================================================
         SETTINGS
         ====================================================== -->

    <main class="view-section" id="view-settings">

        <div class="glass-card settings-card">

            <h2>
                <i class="fa-solid fa-gear"></i>

                <span data-i18n="settingsTitle">
                    App Settings
                </span>
            </h2>


            <div class="settings-group">

                <h3 data-i18n="secAccount">
                    Account Profile
                </h3>

                <div class="input-stacked">

                    <label data-i18n="labelYourName">
                        Your Name
                    </label>

                    <input type="text"
                           id="settingsUserName"
                           placeholder="Enter your name"
                           maxlength="40">

                </div>

            </div>


            <div class="settings-group">

                <h3 data-i18n="secAppearance">
                    Appearance
                </h3>

                <div class="setting-row">

                    <span data-i18n="labelThemeMode">
                        Theme Mode
                    </span>

                    <select id="themeSelectDropdown">

                        <option value="dark">
                            Dark Mode
                        </option>

                        <option value="light">
                            Light Mode
                        </option>

                    </select>

                </div>

            </div>


            <div class="settings-group">

                <h3 data-i18n="secLanguage">
                    Language
                </h3>

                <div class="setting-row">

                    <span data-i18n="labelLanguage">
                        App Language
                    </span>

                    <select id="languageSelect">

                        <option value="en">
                            English
                        </option>

                        <option value="bn">
                            বাংলা
                        </option>

                        <option value="hi">
                            हिन्दी
                        </option>

                    </select>

                </div>

            </div>


            <div class="settings-group">

                <h3 data-i18n="secPrivacy">
                    Privacy & Data
                </h3>

                <button class="btn-danger-outline"
                        id="clearLocalDataBtn"
                        data-i18n="clearLocalData">

                    Clear All Local Data

                </button>

                <p class="privacy-note"
                   data-i18n="privacyNoteText">

                    Client-side application.
                    No remote tracking.
                    Data stays securely in your browser.

                </p>

            </div>


            <div class="settings-group about-group">

                <h3 data-i18n="secAbout">
                    About ResQ
                </h3>

                <p>
                    <strong>ResQ</strong> v2.0
                </p>

                <p class="creator-sign">
                    Designed & Developed by Pritam
                </p>

                <p class="backend-notice"
                   data-i18n="backendNotice">

                    *Note: Real-time cloud sync,
                    actual automated SMS gateways,
                    and cloud user authentication
                    require a backend.

                </p>

            </div>

        </div>

    </main>


    <!-- ======================================================
         SOS MODAL
         ====================================================== -->

    <div class="modal-overlay" id="sosModal">

        <div class="modal-card">

            <div class="modal-header-alert">

                <i class="fa-solid fa-triangle-exclamation"></i>

                <h2 data-i18n="sosAlertActivated">
                    Emergency Alert Activated
                </h2>

            </div>


            <p class="modal-desc"
               data-i18n="sosActionDesc">

                Emergency protocols initiated.
                Verify location and contact dispatch status below:

            </p>


            <div class="modal-checklist">

                <div class="check-item success">

                    <i class="fa-solid fa-circle-check"></i>

                    <span data-i18n="chkSiren">
                        Audio Alarm Triggered
                    </span>

                </div>


                <div class="check-item"
                     id="modalLocStatusCheck">

                    <i class="fa-solid fa-circle-notch fa-spin"></i>

                    <span data-i18n="chkLoc">
                        Attaching GPS Location...
                    </span>

                </div>


                <div class="check-item"
                     id="modalContactStatusCheck">

                    <i class="fa-solid fa-circle-xmark"></i>

                    <span data-i18n="chkContact">
                        No Primary Contact Ready
                    </span>

                </div>

            </div>


            <div class="modal-actions">

                <button class="btn-blue"
                        id="modalWhatsappBtn"
                        disabled>

                    <i class="fa-brands fa-whatsapp"></i>

                    <span data-i18n="sendWhatsapp">
                        Send WhatsApp Alert
                    </span>

                </button>


                <a href="tel:112"
                   class="btn-red-solid">

                    <i class="fa-solid fa-phone"></i>

                    <span data-i18n="call112">
                        Call 112 Emergency
                    </span>

                </a>


                <button class="btn-secondary"
                        id="closeModalBtn"
                        style="padding:10px;border-radius:10px;cursor:pointer;">

                    <span data-i18n="closeModal">
                        Dismiss / Close
                    </span>

                </button>

            </div>

        </div>

    </div>


    <!-- ======================================================
         BOTTOM NAV
         ====================================================== -->

    <nav class="bottom-nav">

        <button class="nav-item active"
                data-view="home">

            <i class="fa-solid fa-house"></i>

            <span data-i18n="navHome">
                Home
            </span>

        </button>


        <button class="nav-item"
                data-view="contacts">

            <i class="fa-solid fa-users"></i>

            <span data-i18n="navContacts">
                Contacts
            </span>

        </button>


        <button class="nav-item"
                data-view="firstaid">

            <i class="fa-solid fa-kit-medical"></i>

            <span data-i18n="navFirstAid">
                First Aid
            </span>

        </button>


        <button class="nav-item"
                data-view="settings">

            <i class="fa-solid fa-gear"></i>

            <span data-i18n="navSettings">
                Settings
            </span>

        </button>

    </nav>

</div>


<script>

/* ==========================================================
   RESQ — SINGLE FILE JAVASCRIPT
   Designed & Developed by Pritam
   ========================================================== */


/* ==========================================================
   TRANSLATIONS
   ========================================================== */

const i18nText = {

    en: {
        splashTag: '"Emergency. Anytime. Anywhere."',
        dashSubtitle: 'Emergency assistance at your fingertips.',
        holdToActivate: 'Hold 3s',
        sosInstruction: 'Press and hold for 3 seconds to trigger emergency alert',
        emergencyHelplines: 'Emergency Helplines (India)',
        helplineDisclaimer: 'Emergency numbers may vary by location. Verify local services before relying on them.',
        liveLocationTitle: 'Live Location',
        gpsStandby: 'Standby',
        locFetchPrompt: 'Click refresh to acquire precise GPS coordinates.',
        btnRefresh: 'Refresh',
        btnMaps: 'Maps',
        btnShare: 'Share',
        trustedContactsTitle: 'Trusted Contacts',
        clearAll: 'Clear All',
        storageNote: 'Your contacts are stored locally on this device via LocalStorage.',
        setPrimary: 'Set as Primary',
        btnAdd: 'Add Contact',
        firstAidTitle: 'First Aid Emergency Guide',
        chipAll: 'All',
        chipBleeding: 'Bleeding',
        chipBurns: 'Burns',
        chipBite: 'Snake Bite',
        chipFaint: 'Fainting',
        settingsTitle: 'App Settings',
        secAccount: 'Account Profile',
        labelYourName: 'Your Name',
        secAppearance: 'Appearance',
        labelThemeMode: 'Theme Mode',
        secLanguage: 'Language',
        labelLanguage: 'App Language',
        secPrivacy: 'Privacy & Data',
        clearLocalData: 'Clear All Local Data',
        privacyNoteText: 'Client-side application. No remote tracking. Data stays securely in your browser.',
        secAbout: 'About ResQ',
        backendNotice: '*Note: Real-time cloud sync, actual automated SMS gateways, and cloud user authentication require a backend.',
        sosAlertActivated: 'Emergency Alert Activated',
        sosActionDesc: 'Emergency protocols initiated. Verify location and contact dispatch status below:',
        chkSiren: 'Audio Alarm Triggered',
        chkLoc: 'Attaching GPS Location...',
        chkContact: 'No Primary Contact Ready',
        sendWhatsapp: 'Send WhatsApp Alert',
        call112: 'Call 112 Emergency',
        closeModal: 'Dismiss / Close',
        navHome: 'Home',
        navContacts: 'Contacts',
        navFirstAid: 'First Aid',
        navSettings: 'Settings'
    },

    bn: {
        splashTag: '"জরুরী সাহায্য। যে কোনো সময়। যে কোনো জায়গায়।"',
        dashSubtitle: 'আপনার হাতের কাছেই জরুরী সহায়তা।',
        holdToActivate: '৩ সেকেন্ড চেপে রাখুন',
        sosInstruction: 'জরুরী অ্যালার্ট চালু করতে ৩ সেকেন্ড প্রেস করে ধরে রাখুন',
        emergencyHelplines: 'জরুরী হেল্পলাইন (ভারত)',
        helplineDisclaimer: 'স্থানীয় এলাকা অনুযায়ী নম্বর পরিবর্তিত হতে পারে। ব্যবহার করার আগে যাচাই করুন।',
        liveLocationTitle: 'লাইভ লোকেশন',
        gpsStandby: 'অপেক্ষমাণ',
        locFetchPrompt: 'সঠিক GPS লোকেশন পেতে রিফ্রেশ করুন।',
        btnRefresh: 'রিফ্রেশ',
        btnMaps: 'ম্যাপস',
        btnShare: 'শেয়ার',
        trustedContactsTitle: 'বিশ্বস্ত যোগাযোগ নম্বর',
        clearAll: 'সব মুছুন',
        storageNote: 'আপনার কন্টাক্টগুলি শুধুমাত্র এই ডিভাইসের LocalStorage-এ সংরক্ষিত থাকে।',
        setPrimary: 'প্রাইমারি সেট করুন',
        btnAdd: 'কন্টাক্ট যোগ করুন',
        firstAidTitle: 'প্রাথমিক চিকিৎসা নির্দেশিকা',
        chipAll: 'সব',
        chipBleeding: 'রক্তপাত',
        chipBurns: 'পোড়া',
        chipBite: 'সাপের কামড়',
        chipFaint: 'অজ্ঞান',
        settingsTitle: 'অ্যাপ সেটিংস',
        secAccount: 'ইউজার প্রোফাইল',
        labelYourName: 'আপনার নাম',
        secAppearance: 'থিম ও প্রদর্শন',
        labelThemeMode: 'থিম মোড',
        secLanguage: 'ভাষা',
        labelLanguage: 'অ্যাপের ভাষা',
        secPrivacy: 'গোপনীয়তা ও ডেটা',
        clearLocalData: 'সমস্ত লোকাল ডেটা মুছুন',
        privacyNoteText: 'ক্লায়েন্ট-সাইড অ্যাপ। কোনো রিমোট ট্র্যাকিং নেই। ডেটা আপনার ব্রাউজারেই থাকে।',
        secAbout: 'ResQ সম্পর্কে',
        backendNotice: '*নোট: ক্লাউড সিঙ্ক, অটোমেটেড SMS এবং ক্লাউড অথেন্টিকেশনের জন্য backend প্রয়োজন।',
        sosAlertActivated: 'জরুরী অ্যালার্ট সক্রিয়',
        sosActionDesc: 'জরুরী প্রোটোকল শুরু হয়েছে। নিচের স্ট্যাটাস দেখুন:',
        chkSiren: 'অডিও অ্যালার্ম চালু হয়েছে',
        chkLoc: 'GPS লোকেশন যুক্ত করা হচ্ছে...',
        chkContact: 'কোনো প্রাইমারি কন্টাক্ট প্রস্তুত নেই',
        sendWhatsapp: 'WhatsApp অ্যালার্ট পাঠান',
        call112: '১১২-এ কল করুন',
        closeModal: 'বন্ধ করুন',
        navHome: 'হোম',
        navContacts: 'কন্টাক্টস',
        navFirstAid: 'ফার্স্ট এইড',
        navSettings: 'সেটিংস'
    },

    hi: {
        splashTag: '"आपातकालीन सहायता। कभी भी। कहीं भी।"',
        dashSubtitle: 'आपकी उंगलियों पर आपातकालीन सहायता।',
        holdToActivate: '3 सेकंड दबाकर रखें',
        sosInstruction: 'आपातकालीन अलर्ट सक्रिय करने के लिए 3 सेकंड तक दबाकर रखें',
        emergencyHelplines: 'आपातकालीन हेल्पलाइन (भारत)',
        helplineDisclaimer: 'स्थान के अनुसार नंबर भिन्न हो सकते हैं। उपयोग करने से पहले सत्यापित करें।',
        liveLocationTitle: 'लाइव लोकेशन',
        gpsStandby: 'तैयार',
        locFetchPrompt: 'सटीक GPS लोकेशन प्राप्त करने के लिए रिफ्रेश करें।',
        btnRefresh: 'रिफ्रेश',
        btnMaps: 'मैप्स',
        btnShare: 'शेयर',
        trustedContactsTitle: 'विश्वसनीय संपर्क',
        clearAll: 'सभी हटाएं',
        storageNote: 'आपके संपर्क इस डिवाइस के LocalStorage में सुरक्षित रहते हैं।',
        setPrimary: 'प्राथमिक सेट करें',
        btnAdd: 'संपर्क जोड़ें',
        firstAidTitle: 'प्राथमिक चिकित्सा मार्गदर्शिका',
        chipAll: 'सभी',
        chipBleeding: 'रक्तस्राव',
        chipBurns: 'जलना',
        chipBite: 'सांप का काटना',
        chipFaint: 'बेहोशी',
        settingsTitle: 'ऐप सेटिंग्स',
        secAccount: 'प्रोफाइल',
        labelYourName: 'आपका नाम',
        secAppearance: 'दिखावट',
        labelThemeMode: 'थीम मोड',
        secLanguage: 'भाषा',
        labelLanguage: 'ऐप की भाषा',
        secPrivacy: 'गोपनीयता और डेटा',
        clearLocalData: 'सभी स्थानीय डेटा साफ़ करें',
        privacyNoteText: 'क्लाइंट-साइड ऐप। कोई रिमोट ट्रैकिंग नहीं। डेटा आपके ब्राउज़र में सुरक्षित रहता है।',
        secAbout: 'ResQ के बारे में',
        backendNotice: '*नोट: क्लाउड सिंक, स्वचालित SMS और क्लाउड ऑथेंटिकेशन के लिए backend आवश्यक है।',
        sosAlertActivated: 'आपातकालीन अलर्ट सक्रिय',
        sosActionDesc: 'आपातकालीन प्रोटोकॉल शुरू हो गए हैं। नीचे स्थिति जांचें:',
        chkSiren: 'ऑडियो सायरन सक्रिय',
        chkLoc: 'GPS लोकेशन जोड़ी जा रही है...',
        chkContact: 'कोई प्राथमिक संपर्क तैयार नहीं',
        sendWhatsapp: 'WhatsApp अलर्ट भेजें',
        call112: '112 आपातकालीन कॉल करें',
        closeModal: 'बंद करें',
        navHome: 'होम',
        navContacts: 'संपर्क',
        navFirstAid: 'प्र. चिकित्सा',
        navSettings: 'सेटिंग्स'
    }

};


/* ==========================================================
   FIRST AID DATABASE
   ========================================================== */

const firstAidDatabase = [

    {
        id: 'bleeding',
        category: 'bleeding',
        title: 'Severe Bleeding (রক্তপাত / गंभीर रक्तस्राव)',
        whatToDo: 'Apply firm, continuous pressure to the wound using clean cloth or sterile dressing. If blood soaks through, add more material without removing the first layer.',
        whatNotToDo: 'Do not remove an object embedded in the wound. Do not use dirty material directly on the wound.',
        whenToCall: 'Call emergency services for heavy or uncontrolled bleeding, signs of shock, or a serious wound.'
    },

    {
        id: 'burns',
        category: 'burns',
        title: 'Burns & Scalds (পোড়া / जलना)',
        whatToDo: 'Cool the burn under cool running water for about 20 minutes as soon as possible. Remove nearby jewellery or clothing unless stuck to the skin. Cover loosely with a clean non-fluffy dressing.',
        whatNotToDo: 'Do not use ice, butter, toothpaste, oil or creams on a fresh burn. Do not burst blisters.',
        whenToCall: 'Seek urgent medical help for large, deep or serious burns, burns involving the face, hands, major joints or genitals, or electrical/chemical burns.'
    },

    {
        id: 'snakeBite',
        category: 'poison',
        title: 'Snake Bite (সাপের কামড় / सांप का काटना)',
        whatToDo: 'Keep the person calm and as still as possible. Immobilize the bitten limb. Remove rings, watches and other tight items. Get emergency medical help immediately.',
        whatNotToDo: 'Do not cut the bite, suck venom, apply ice, or use a tight tourniquet. Do not attempt to catch the snake.',
        whenToCall: 'Get emergency medical care immediately. Antivenom and hospital treatment may be required.'
    },

    {
        id: 'faint',
        category: 'faint',
        title: 'Fainting & Unconsciousness (অজ্ঞান / बेहोशी)',
        whatToDo: 'If the person is breathing normally, lay them flat and keep the airway clear. If unconscious but breathing, place them in the recovery position and monitor breathing.',
        whatNotToDo: 'Do not give food, drink or medicine to an unconscious person. Do not leave an unconscious person alone.',
        whenToCall: 'Call emergency services if the person is not breathing normally, does not quickly regain consciousness, has a serious injury, seizure, chest pain, or repeated fainting.'
    }

];


/* ==========================================================
   STATE
   ========================================================== */

let currentGlobalLat = null;
let currentGlobalLon = null;
let currentGlobalMapLink = '';

let sosIntervalTimer = null;
let sosTriggered = false;
let holdProgress = 0;

let audioContextInstance = null;

let currentAidCategory = 'all';

let activeSosTargetPhone = null;


/* ==========================================================
   DOM READY
   ========================================================== */

document.addEventListener('DOMContentLoaded', () => {

    initSplash();

    loadUserSettings();

    renderContactsList();

    renderFirstAidGuides(firstAidDatabase);

    setupEventListeners();

    checkNetworkStatus();

    window.addEventListener('online', checkNetworkStatus);
    window.addEventListener('offline', checkNetworkStatus);

});


/* ==========================================================
   EVENT LISTENERS
   ========================================================== */

function setupEventListeners() {

    document
        .getElementById('themeToggleBtn')
        .addEventListener('click', toggleTheme);


    document
        .getElementById('themeSelectDropdown')
        .addEventListener('change', function() {
            changeThemeMode(this.value);
        });


    document
        .getElementById('languageSelect')
        .addEventListener('change', function() {
            changeLanguage(this.value);
        });


    document
        .getElementById('settingsUserName')
        .addEventListener('change', saveUserProfile);


    document
        .getElementById('refreshLocationBtn')
        .addEventListener('click', fetchLiveLocation);


    document
        .getElementById('mapOpenBtn')
        .addEventListener('click', openGoogleMaps);


    document
        .getElementById('shareLocBtn')
        .addEventListener('click', shareLocation);


    document
        .getElementById('contactForm')
        .addEventListener('submit', handleContactSubmit);


    document
        .getElementById('clearContactsBtn')
        .addEventListener('click', clearAllContacts);


    document
        .getElementById('clearLocalDataBtn')
        .addEventListener('click', clearAllLocalData);


    document
        .getElementById('firstAidSearch')
        .addEventListener('input', filterFirstAidGuides);


    document
        .getElementById('closeModalBtn')
        .addEventListener('click', closeSosModal);


    document
        .getElementById('modalWhatsappBtn')
        .addEventListener('click', dispatchWhatsappSOS);


    document.querySelectorAll('.nav-item').forEach(btn => {

        btn.addEventListener('click', () => {

            switchView(
                btn.dataset.view,
                btn
            );

        });

    });


    document.querySelectorAll('.chip').forEach(chip => {

        chip.addEventListener('click', () => {

            filterChip(
                chip.dataset.category,
                chip
            );

        });

    });


    setupSOSButton();

}


/* ==========================================================
   SPLASH
   ========================================================== */

function initSplash() {

    const splash = document.getElementById('splashScreen');

    setTimeout(() => {

        splash.classList.add('hidden');

    }, 2400);

}


/* ==========================================================
   NAVIGATION
   ========================================================== */

function switchView(viewName, btnElement) {

    document
        .querySelectorAll('.view-section')
        .forEach(el => el.classList.remove('active'));

    document
        .querySelectorAll('.bottom-nav .nav-item')
        .forEach(el => el.classList.remove('active'));

    const target = document.getElementById(`view-${viewName}`);

    if (target) {
        target.classList.add('active');
    }

    if (btnElement) {
        btnElement.classList.add('active');
    }

}


/* ==========================================================
   THEME
   ========================================================== */

function toggleTheme() {

    const currentTheme =
        document.documentElement.getAttribute('data-theme');

    const newTheme =
        currentTheme === 'dark' ? 'light' : 'dark';

    changeThemeMode(newTheme);

}


function changeThemeMode(theme) {

    if (theme !== 'dark' && theme !== 'light') {
        theme = 'dark';
    }

    document.documentElement
        .setAttribute('data-theme', theme);

    const icon =
        document.getElementById('themeIcon');

    icon.className =
        theme === 'dark'
            ? 'fa-solid fa-moon'
            : 'fa-solid fa-sun';

    document.getElementById('themeSelectDropdown').value = theme;

    localStorage.setItem('resq_theme', theme);

}


/* ==========================================================
   LANGUAGE
   ========================================================== */

function changeLanguage(langCode) {

    if (!i18nText[langCode]) {
        langCode = 'en';
    }

    localStorage.setItem('resq_lang', langCode);

    applyTranslations(langCode);

    renderContactsList();

    applyPlaceholders(langCode);

}


function applyTranslations(lang) {

    const dict =
        i18nText[lang] || i18nText.en;

    document
        .querySelectorAll('[data-i18n]')
        .forEach(el => {

            const key =
                el.getAttribute('data-i18n');

            if (dict[key]) {
                el.textContent = dict[key];
            }

        });

}


function applyPlaceholders(lang) {

    const placeholders = {

        en: {
            name: 'Contact Name',
            phone: '10-digit Mobile No.',
            search: 'Search condition (e.g. Bleeding, Burns)...',
            username: 'Enter your name'
        },

        bn: {
            name: 'কন্টাক্টের নাম',
            phone: '১০ সংখ্যার মোবাইল নম্বর',
            search: 'সমস্যা খুঁজুন (যেমন: রক্তপাত, পোড়া)...',
            username: 'আপনার নাম লিখুন'
        },

        hi: {
            name: 'संपर्क का नाम',
            phone: '10 अंकों का मोबाइल नंबर',
            search: 'समस्या खोजें (जैसे रक्तस्राव, जलना)...',
            username: 'अपना नाम दर्ज करें'
        }

    };

    const p =
        placeholders[lang] || placeholders.en;

    document.getElementById('cName').placeholder = p.name;
    document.getElementById('cPhone').placeholder = p.phone;
    document.getElementById('firstAidSearch').placeholder = p.search;
    document.getElementById('settingsUserName').placeholder = p.username;

}


/* ==========================================================
   SETTINGS
   ========================================================== */

function loadUserSettings() {

    const savedTheme =
        localStorage.getItem('resq_theme') || 'dark';

    changeThemeMode(savedTheme);


    const savedLang =
        localStorage.getItem('resq_lang') || 'en';

    document.getElementById('languageSelect').value =
        savedLang;

    applyTranslations(savedLang);
    applyPlaceholders(savedLang);


    const savedName =
        localStorage.getItem('resq_username') || '';

    document.getElementById('settingsUserName').value =
        savedName;

    updateGreetingDisplay(savedName);

}


function saveUserProfile() {

    const name =
        document
            .getElementById('settingsUserName')
            .value
            .trim()
            .slice(0,40);

    localStorage.setItem(
        'resq_username',
        name
    );

    updateGreetingDisplay(name);

}


function updateGreetingDisplay(name) {

    const display =
        document.getElementById('userGreetingDisplay');

    if (name) {

        display.textContent =
            `Stay Safe, ${name}`;

    } else {

        display.textContent =
            'Stay Safe';

    }

}


/* ==========================================================
   SOS SYSTEM
   ========================================================== */

function setupSOSButton() {

    const btn =
        document.getElementById('sosMainBtn');

    btn.addEventListener(
        'pointerdown',
        startSosHold
    );

    btn.addEventListener(
        'pointerup',
        cancelSosHold
    );

    btn.addEventListener(
        'pointercancel',
        cancelSosHold
    );

    btn.addEventListener(
        'pointerleave',
        cancelSosHold
    );

}


function startSosHold(event) {

    if (sosTriggered) {
        return;
    }

    event.preventDefault();

    if (sosIntervalTimer) {
        clearInterval(sosIntervalTimer);
    }

    holdProgress = 0;

    const progressBar =
        document.getElementById('sosProgress');

    const instruction =
        document.getElementById('sosInstructionText');

    instruction.textContent =
        'Holding... Keep pressing!';


    sosIntervalTimer =
        setInterval(() => {

            holdProgress += 100 / 30;

            progressBar.style.width =
                `${Math.min(holdProgress,100)}%`;


            if (holdProgress >= 100) {

                clearInterval(sosIntervalTimer);

                sosIntervalTimer = null;

                sosTriggered = true;

                triggerActualSOS();

            }

        }, 100);

}


function cancelSosHold() {

    if (sosTriggered) {
        return;
    }

    if (sosIntervalTimer) {

        clearInterval(sosIntervalTimer);

        sosIntervalTimer = null;

    }

    holdProgress = 0;

    const progress =
        document.getElementById('sosProgress');

    if (progress) {
        progress.style.width = '0%';
    }

    const lang =
        localStorage.getItem('resq_lang') || 'en';

    document.getElementById('sosInstructionText')
        .textContent =
        i18nText[lang].sosInstruction;

}


function triggerActualSOS() {

    playEmergencySiren();

    const modal =
        document.getElementById('sosModal');

    modal.classList.add('active');

    updateSOSLocationStatus();

    updateSOSContactStatus();

}


function updateSOSLocationStatus() {

    const locCheck =
        document.getElementById('modalLocStatusCheck');

    if (currentGlobalMapLink) {

        locCheck.innerHTML = `
            <i class="fa-solid fa-circle-check"></i>
            <span>GPS Location Attached</span>
        `;

        locCheck.className =
            'check-item success';

    } else {

        locCheck.innerHTML = `
            <i class="fa-solid fa-triangle-exclamation"></i>
            <span>Location unavailable</span>
        `;

        locCheck.className =
            'check-item';

    }

}


function updateSOSContactStatus() {

    const contactCheck =
        document.getElementById('modalContactStatusCheck');

    const waBtn =
        document.getElementById('modalWhatsappBtn');

    let contacts = [];

    try {

        contacts =
            JSON.parse(
                localStorage.getItem('resq_contacts')
            ) || [];

    } catch {

        contacts = [];

    }


    const primary =
        contacts.find(c => c.primary) ||
        contacts[0];


    if (primary) {

        activeSosTargetPhone =
            primary.phone;

        contactCheck.innerHTML = `
            <i class="fa-solid fa-circle-check"></i>
            <span>Primary Contact Ready (${escapeHTML(primary.name)})</span>
        `;

        contactCheck.className =
            'check-item success';

        waBtn.disabled = false;

    } else {

        activeSosTargetPhone = null;

        contactCheck.innerHTML = `
            <i class="fa-solid fa-circle-xmark"></i>
            <span>No Trusted Contact Configured</span>
        `;

        contactCheck.className =
            'check-item';

        waBtn.disabled = true;

    }

}


function closeSosModal() {

    document
        .getElementById('sosModal')
        .classList.remove('active');

    sosTriggered = false;

    holdProgress = 0;

    document
        .getElementById('sosProgress')
        .style.width = '0%';

}


function dispatchWhatsappSOS() {

    if (!activeSosTargetPhone) {
        return;
    }

    let message =
        'EMERGENCY! I need immediate assistance.';

    if (currentGlobalMapLink) {

        message +=
            '\nMy GPS location: ' +
            currentGlobalMapLink;

    }


    const url =
        `https://wa.me/91${activeSosTargetPhone}?text=${
            encodeURIComponent(message)
        }`;


    window.open(
        url,
        '_blank',
        'noopener,noreferrer'
    );

}


/* ==========================================================
   AUDIO SIREN
   ========================================================== */

function playEmergencySiren() {

    try {

        if (!audioContextInstance) {

            audioContextInstance =
                new (
                    window.AudioContext ||
                    window.webkitAudioContext
                )();

        }

        if (audioContextInstance.state === 'suspended') {
            audioContextInstance.resume();
        }


        const osc =
            audioContextInstance.createOscillator();

        const gain =
            audioContextInstance.createGain();


        osc.type = 'sawtooth';

        osc.frequency.setValueAtTime(
            500,
            audioContextInstance.currentTime
        );

        osc.frequency.linearRampToValueAtTime(
            900,
            audioContextInstance.currentTime + .4
        );


        gain.gain.setValueAtTime(
            .2,
            audioContextInstance.currentTime
        );

        gain.gain.exponentialRampToValueAtTime(
            .01,
            audioContextInstance.currentTime + .4
        );


        osc.connect(gain);

        gain.connect(
            audioContextInstance.destination
        );


        osc.start();

        osc.stop(
            audioContextInstance.currentTime + .4
        );

    } catch (error) {

        console.log(
            'Audio unavailable.'
        );

    }

}


/* ==========================================================
   LOCATION
   ========================================================== */

function fetchLiveLocation() {

    const statusBox =
        document.getElementById('locationStatusBox');

    const badge =
        document.getElementById('gpsStatusBadge');

    const metaInfo =
        document.getElementById('locationMetaInfo');

    const mapBtn =
        document.getElementById('mapOpenBtn');

    const shareBtn =
        document.getElementById('shareLocBtn');


    if (!navigator.geolocation) {

        badge.textContent =
            'Unsupported';

        statusBox.innerHTML =
            '<span style="color:var(--accent-red)">Geolocation is not supported by this browser.</span>';

        return;

    }


    badge.textContent =
        'Acquiring...';

    badge.style.background =
        'rgba(59,130,246,.15)';

    badge.style.color =
        'var(--accent-blue)';


    statusBox.innerHTML =
        '<i class="fa-solid fa-spinner fa-spin"></i> Fetching GPS location...';


    navigator.geolocation.getCurrentPosition(

        position => {

            currentGlobalLat =
                position.coords.latitude;

            currentGlobalLon =
                position.coords.longitude;


            const accuracy =
                Number(position.coords.accuracy)
                    .toFixed(1);


            const timestamp =
                new Date()
                    .toLocaleTimeString();


            currentGlobalMapLink =
                `https://maps.google.com/?q=${currentGlobalLat},${currentGlobalLon}`;


            badge.textContent =
                'GPS Ready';

            badge.style.background =
                'rgba(16,185,129,.15)';

            badge.style.color =
                'var(--accent-green)';


            statusBox.innerHTML =
                '<strong>GPS coordinates successfully acquired.</strong>';


            metaInfo.style.display =
                'flex';


            document.getElementById('locLatLon')
                .textContent =
                `Lat: ${currentGlobalLat.toFixed(5)}, Lon: ${currentGlobalLon.toFixed(5)}`;


            document.getElementById('locAccuracy')
                .textContent =
                `Accuracy: ±${accuracy}m`;


            document.getElementById('locTime')
                .textContent =
                `Updated: ${timestamp}`;


            mapBtn.disabled = false;

            shareBtn.disabled = false;

        },

        error => {

            currentGlobalLat = null;
            currentGlobalLon = null;
            currentGlobalMapLink = '';

            badge.textContent =
                'Unavailable';

            badge.style.background =
                'rgba(239,68,68,.15)';

            badge.style.color =
                'var(--accent-red)';


            statusBox.innerHTML =
                '<span style="color:var(--accent-red)">Location permission is unavailable or GPS signal could not be acquired. Enable location permission and try again.</span>';


            metaInfo.style.display =
                'none';

            mapBtn.disabled = true;

            shareBtn.disabled = true;

        },

        {
            enableHighAccuracy: true,
            timeout: 12000,
            maximumAge: 0
        }

    );

}


function openGoogleMaps() {

    if (!currentGlobalMapLink) {
        return;
    }

    window.open(
        currentGlobalMapLink,
        '_blank',
        'noopener,noreferrer'
    );

}


async function shareLocation() {

    if (!currentGlobalMapLink) {
        return;
    }


    if (navigator.share) {

        try {

            await navigator.share({

                title: 'ResQ Emergency Location',

                text:
                    'I need emergency assistance. Here is my GPS location:',

                url:
                    currentGlobalMapLink

            });

        } catch {

            // User cancelled share.

        }

        return;

    }


    try {

        await navigator.clipboard.writeText(
            currentGlobalMapLink
        );

        alert(
            'Location map link copied to clipboard.'
        );

    } catch {

        alert(
            currentGlobalMapLink
        );

    }

}


/* ==========================================================
   CONTACT MANAGEMENT
   ========================================================== */

function getContacts() {

    try {

        const data =
            JSON.parse(
                localStorage.getItem('resq_contacts')
            );

        return Array.isArray(data)
            ? data
            : [];

    } catch {

        return [];

    }

}


function saveContacts(contacts) {

    localStorage.setItem(
        'resq_contacts',
        JSON.stringify(contacts)
    );

}


function handleContactSubmit(event) {

    event.preventDefault();


    const nameInput =
        document.getElementById('cName');

    const phoneInput =
        document.getElementById('cPhone');

    const primaryCheck =
        document.getElementById('cPrimary');


    const name =
        nameInput.value.trim().slice(0,50);

    const phone =
        phoneInput.value.trim();


    if (!name) {

        alert('Please enter the contact name.');

        return;

    }


    if (!/^[0-9]{10}$/.test(phone)) {

        alert(
            'Please enter a valid 10-digit Indian mobile number.'
        );

        return;

    }


    let contacts =
        getContacts();


    if (
        contacts.some(
            contact => contact.phone === phone
        )
    ) {

        alert(
            'This phone number is already saved.'
        );

        return;

    }


    if (primaryCheck.checked) {

        contacts.forEach(
            contact => contact.primary = false
        );

    }


    contacts.push({

        id:
            Date.now().toString(),

        name:
            name,

        phone:
            phone,

        primary:
            primaryCheck.checked ||
            contacts.length === 0

    });


    saveContacts(contacts);


    nameInput.value = '';

    phoneInput.value = '';

    primaryCheck.checked = false;


    renderContactsList();

}


function removeContact(index) {

    const contacts =
        getContacts();


    if (
        index < 0 ||
        index >= contacts.length
    ) {
        return;
    }


    contacts.splice(index,1);


    if (
        contacts.length > 0 &&
        !contacts.some(c => c.primary)
    ) {

        contacts[0].primary = true;

    }


    saveContacts(contacts);

    renderContactsList();

}


function clearAllContacts() {

    if (
        !confirm(
            'Are you sure you want to delete all saved trusted contacts?'
        )
    ) {
        return;
    }


    localStorage.removeItem(
        'resq_contacts'
    );


    renderContactsList();

}


function renderContactsList() {

    const container =
        document.getElementById(
            'contactsListContainer'
        );


    const contacts =
        getContacts();


    container.innerHTML = '';


    if (!contacts.length) {

        container.innerHTML = `
            <p style="
                font-size:12px;
                color:var(--text-sub);
                text-align:center;
                padding:15px;
            ">
                No trusted contacts added yet.
            </p>
        `;

        return;

    }


    contacts.forEach((contact,index) => {

        const card =
            document.createElement('div');

        card.className =
            'contact-item-card';


        const info =
            document.createElement('div');

        info.className =
            'contact-info-block';


        const name =
            document.createElement('span');

        name.textContent =
            contact.name;


        if (contact.primary) {

            const badge =
                document.createElement('span');

            badge.className =
                'badge-primary';

            badge.textContent =
                'Primary';

            name.appendChild(badge);

        }


        const phone =
            document.createElement('small');

        phone.textContent =
            `+91 ${contact.phone}`;


        info.appendChild(name);

        info.appendChild(phone);


        const actions =
            document.createElement('div');

        actions.className =
            'contact-actions';


        const call =
            document.createElement('button');

        call.className =
            'call-icon';

        call.title =
            'Call';

        call.innerHTML =
            '<i class="fa-solid fa-phone"></i>';

        call.addEventListener(
            'click',
            () => {
                window.location.href =
                    `tel:${contact.phone}`;
            }
        );


        const whatsapp =
            document.createElement('button');

        whatsapp.className =
            'wa-icon';

        whatsapp.title =
            'WhatsApp';

        whatsapp.innerHTML =
            '<i class="fa-brands fa-whatsapp"></i>';

        whatsapp.addEventListener(
            'click',
            () => {

                const url =
                    `https://wa.me/91${contact.phone}?text=${
                        encodeURIComponent(
                            'EMERGENCY! Need help.'
                        )
                    }`;

                window.open(
                    url,
                    '_blank',
                    'noopener,noreferrer'
                );

            }
        );


        const del =
            document.createElement('button');

        del.className =
            'del-icon';

        del.title =
            'Delete';

        del.innerHTML =
            '<i class="fa-solid fa-trash"></i>';

        del.addEventListener(
            'click',
            () => removeContact(index)
        );


        actions.appendChild(call);
        actions.appendChild(whatsapp);
        actions.appendChild(del);


        card.appendChild(info);
        card.appendChild(actions);


        container.appendChild(card);

    });

}


/* ==========================================================
   FIRST AID
   ========================================================== */

function renderFirstAidGuides(guides) {

    const accordion =
        document.getElementById(
            'firstAidAccordion'
        );


    accordion.innerHTML = '';


    if (!guides.length) {

        accordion.innerHTML = `
            <p style="
                font-size:12px;
                color:var(--text-sub);
                text-align:center;
                padding:15px;
            ">
                No matching first-aid guide found.
            </p>
        `;

        return;

    }


    guides.forEach((guide,index) => {

        const card =
            document.createElement('div');

        card.className =
            'accordion-card';


        const header =
            document.createElement('div');

        header.className =
            'accordion-header';


        const title =
            document.createElement('span');

        title.textContent =
            guide.title;


        const icon =
            document.createElement('i');

        icon.className =
            'fa-solid fa-chevron-down';


        header.appendChild(title);
        header.appendChild(icon);


        const body =
            document.createElement('div');

        body.className =
            'accordion-body';


        body.innerHTML = `
            <span class="aid-section-title">
                WHAT TO DO:
            </span>

            <p>${escapeHTML(guide.whatToDo)}</p>

            <span class="aid-section-title"
                  style="color:var(--accent-red)">
                WHAT NOT TO DO:
            </span>

            <p>${escapeHTML(guide.whatNotToDo)}</p>

            <span class="aid-section-title"
                  style="color:var(--accent-blue)">
                WHEN TO CALL EMERGENCY:
            </span>

            <p>${escapeHTML(guide.whenToCall)}</p>
        `;


        header.addEventListener(
            'click',
            () => {

                card.classList.toggle('open');

                icon.className =
                    card.classList.contains('open')
                        ? 'fa-solid fa-chevron-up'
                        : 'fa-solid fa-chevron-down';

            }
        );


        card.appendChild(header);

        card.appendChild(body);

        accordion.appendChild(card);

    });

}


function filterFirstAidGuides() {

    const query =
        document
            .getElementById('firstAidSearch')
            .value
            .toLowerCase()
            .trim();


    let filtered =
        firstAidDatabase;


    if (currentAidCategory !== 'all') {

        filtered =
            filtered.filter(
                guide =>
                    guide.category ===
                    currentAidCategory
            );

    }


    if (query) {

        filtered =
            filtered.filter(guide => {

                const searchable =
                    (
                        guide.title +
                        ' ' +
                        guide.whatToDo +
                        ' ' +
                        guide.whatNotToDo +
                        ' ' +
                        guide.whenToCall
                    ).toLowerCase();

                return searchable.includes(query);

            });

    }


    renderFirstAidGuides(filtered);

}


function filterChip(category, button) {

    currentAidCategory =
        category;


    document
        .querySelectorAll('.filter-chips .chip')
        .forEach(
            chip =>
                chip.classList.remove('active')
        );


    button.classList.add('active');


    filterFirstAidGuides();

}


/* ==========================================================
   LOCAL DATA
   ========================================================== */

function clearAllLocalData() {

    if (
        !confirm(
            'Are you sure you want to clear all local app data and settings?'
        )
    ) {
        return;
    }


    localStorage.clear();

    location.reload();

}


/* ==========================================================
   NETWORK STATUS
   ========================================================== */

function checkNetworkStatus() {

    const indicator =
        document.getElementById(
            'netStatusIndicator'
        );


    if (navigator.onLine) {

        indicator.innerHTML =
            '<i class="fa-solid fa-wifi" style="color:var(--accent-green)"></i>';

        indicator.title =
            'Online';

    } else {

        indicator.innerHTML =
            '<i class="fa-solid fa-triangle-exclamation" style="color:var(--accent-yellow)"></i>';

        indicator.title =
            'Offline mode';

    }

}


/* ==========================================================
   SECURITY HELPER
   ========================================================== */

function escapeHTML(value) {

    const div =
        document.createElement('div');

    div.textContent =
        String(value ?? '');

    return div.innerHTML;

}

</script>

</body>
</html>
