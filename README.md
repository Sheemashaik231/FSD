<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>StudentIQ — Performance Prediction System</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:wght@300;400;500&family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,700;1,9..144,300&display=swap" rel="stylesheet">
<style>
:root {
  --ink: #0a0a0f;
  --paper: #f5f2eb;
  --cream: #ede9df;
  --accent: #c84b1e;
  --accent2: #1e5fc8;
  --gold: #c4922a;
  --muted: #7a7468;
  --border: #d4cfc5;
  --card: #faf9f5;
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

html { scroll-behavior: smooth; }

body {
  font-family: 'DM Mono', monospace;
  background: var(--paper);
  color: var(--ink);
  overflow-x: hidden;
  cursor: none;
}

/* Custom Cursor */
.cursor {
  position: fixed;
  width: 10px; height: 10px;
  background: var(--accent);
  border-radius: 50%;
  pointer-events: none;
  z-index: 9999;
  transform: translate(-50%, -50%);
  transition: transform 0.1s ease, width 0.2s, height 0.2s;
}
.cursor-ring {
  position: fixed;
  width: 32px; height: 32px;
  border: 1.5px solid var(--accent);
  border-radius: 50%;
  pointer-events: none;
  z-index: 9998;
  transform: translate(-50%, -50%);
  transition: all 0.15s ease;
  opacity: 0.6;
}

/* NAV */
nav {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 100;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.2rem 3rem;
  background: rgba(245, 242, 235, 0.85);
  backdrop-filter: blur(12px);
  border-bottom: 1px solid var(--border);
}

.nav-logo {
  font-family: 'Syne', sans-serif;
  font-weight: 800;
  font-size: 1.1rem;
  letter-spacing: -0.02em;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}
.nav-logo span { color: var(--accent); }

.nav-links {
  display: flex;
  gap: 2rem;
  list-style: none;
}
.nav-links a {
  text-decoration: none;
  color: var(--muted);
  font-size: 0.75rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  transition: color 0.2s;
}
.nav-links a:hover { color: var(--accent); }

.nav-badge {
  font-size: 0.7rem;
  background: var(--ink);
  color: var(--paper);
  padding: 0.3rem 0.8rem;
  letter-spacing: 0.05em;
}

/* HERO */
.hero {
  min-height: 100vh;
  display: grid;
  grid-template-columns: 1fr 1fr;
  position: relative;
  overflow: hidden;
}

.hero-left {
  padding: 10rem 3rem 5rem 3rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  position: relative;
  z-index: 2;
}

.hero-tag {
  font-size: 0.7rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 1.5rem;
  display: flex;
  align-items: center;
  gap: 0.8rem;
}
.hero-tag::before {
  content: '';
  display: block;
  width: 2rem;
  height: 1px;
  background: var(--accent);
}

.hero-title {
  font-family: 'Fraunces', serif;
  font-size: clamp(3rem, 5vw, 5.5rem);
  font-weight: 700;
  line-height: 1.0;
  letter-spacing: -0.03em;
  margin-bottom: 1.5rem;
}
.hero-title em {
  font-style: italic;
  color: var(--accent);
}

.hero-desc {
  font-size: 0.85rem;
  line-height: 1.8;
  color: var(--muted);
  max-width: 420px;
  margin-bottom: 2.5rem;
}

.hero-buttons {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
}
.btn-primary {
  background: var(--ink);
  color: var(--paper);
  padding: 0.9rem 2rem;
  font-family: 'DM Mono', monospace;
  font-size: 0.75rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  border: none;
  cursor: none;
  transition: all 0.25s;
  text-decoration: none;
  display: inline-block;
}
.btn-primary:hover { background: var(--accent); transform: translateY(-2px); }

.btn-secondary {
  background: transparent;
  color: var(--ink);
  padding: 0.9rem 2rem;
  font-family: 'DM Mono', monospace;
  font-size: 0.75rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  border: 1.5px solid var(--ink);
  cursor: none;
  transition: all 0.25s;
  text-decoration: none;
  display: inline-block;
}
.btn-secondary:hover { background: var(--ink); color: var(--paper); transform: translateY(-2px); }

.hero-stats {
  margin-top: 4rem;
  display: flex;
  gap: 3rem;
  padding-top: 2rem;
  border-top: 1px solid var(--border);
}
.stat-item { }
.stat-number {
  font-family: 'Fraunces', serif;
  font-size: 2.2rem;
  font-weight: 700;
  color: var(--accent);
  line-height: 1;
}
.stat-label {
  font-size: 0.7rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--muted);
  margin-top: 0.3rem;
}

/* HERO RIGHT */
.hero-right {
  background: var(--ink);
  position: relative;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}

.hero-visual {
  position: relative;
  width: 380px;
}

.model-cards {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
.model-card {
  background: rgba(255,255,255,0.05);
  border: 1px solid rgba(255,255,255,0.1);
  padding: 1.2rem 1.5rem;
  display: flex;
  align-items: center;
  gap: 1.2rem;
  animation: slideIn 0.6s ease forwards;
  opacity: 0;
}
.model-card:nth-child(1) { animation-delay: 0.2s; }
.model-card:nth-child(2) { animation-delay: 0.4s; }
.model-card:nth-child(3) { animation-delay: 0.6s; }
.model-card:nth-child(4) { animation-delay: 0.8s; }

@keyframes slideIn {
  from { opacity: 0; transform: translateX(30px); }
  to   { opacity: 1; transform: translateX(0); }
}

.model-icon {
  width: 36px; height: 36px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.9rem;
  flex-shrink: 0;
}
.model-info { flex: 1; }
.model-name {
  font-family: 'Syne', sans-serif;
  font-size: 0.8rem;
  font-weight: 700;
  color: #fff;
  letter-spacing: 0.03em;
}
.model-sub {
  font-size: 0.65rem;
  color: rgba(255,255,255,0.4);
  margin-top: 0.2rem;
}
.model-acc {
  font-family: 'Fraunces', serif;
  font-size: 1.4rem;
  font-weight: 700;
  line-height: 1;
}

.hero-grid-bg {
  position: absolute;
  inset: 0;
  background-image: linear-gradient(rgba(255,255,255,0.03) 1px, transparent 1px),
                    linear-gradient(90deg, rgba(255,255,255,0.03) 1px, transparent 1px);
  background-size: 40px 40px;
}

/* SECTION WRAPPER */
section {
  padding: 7rem 3rem;
}
.section-label {
  font-size: 0.7rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 1rem;
  display: flex;
  align-items: center;
  gap: 0.8rem;
}
.section-label::before {
  content: '';
  display: block;
  width: 1.5rem;
  height: 1px;
  background: var(--accent);
}
.section-title {
  font-family: 'Fraunces', serif;
  font-size: clamp(2rem, 3.5vw, 3.2rem);
  font-weight: 700;
  letter-spacing: -0.02em;
  line-height: 1.1;
  margin-bottom: 1rem;
}
.section-title em { font-style: italic; color: var(--accent); }

/* ABSTRACT */
.abstract-section {
  background: var(--cream);
  border-top: 1px solid var(--border);
  border-bottom: 1px solid var(--border);
}
.abstract-grid {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 5rem;
  max-width: 1200px;
  margin: 0 auto;
}
.abstract-text {
  font-size: 0.9rem;
  line-height: 2;
  color: var(--muted);
}
.abstract-text p + p { margin-top: 1.2rem; }
.keyword-list {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-top: 2rem;
}
.keyword {
  font-size: 0.7rem;
  letter-spacing: 0.05em;
  padding: 0.3rem 0.8rem;
  background: var(--ink);
  color: var(--paper);
}

/* PIPELINE */
.pipeline-section { background: var(--paper); }
.pipeline-section .inner { max-width: 1200px; margin: 0 auto; }
.pipeline-steps {
  display: grid;
  grid-template-columns: repeat(7, 1fr);
  gap: 0;
  margin-top: 4rem;
  position: relative;
}
.pipeline-steps::before {
  content: '';
  position: absolute;
  top: 2.2rem;
  left: 5%;
  right: 5%;
  height: 1px;
  background: var(--border);
  z-index: 0;
}
.pipe-step {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  text-align: center;
  position: relative;
  z-index: 1;
  padding: 0 0.5rem;
  opacity: 0;
  transform: translateY(20px);
  transition: all 0.5s ease;
}
.pipe-step.visible { opacity: 1; transform: translateY(0); }
.pipe-num {
  width: 2.8rem; height: 2.8rem;
  border-radius: 50%;
  background: var(--paper);
  border: 2px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.75rem;
  font-weight: 500;
  transition: all 0.3s;
}
.pipe-step:hover .pipe-num {
  background: var(--accent);
  border-color: var(--accent);
  color: white;
}
.pipe-title {
  font-family: 'Syne', sans-serif;
  font-size: 0.7rem;
  font-weight: 700;
  letter-spacing: 0.03em;
  text-transform: uppercase;
  line-height: 1.3;
}
.pipe-sub {
  font-size: 0.65rem;
  color: var(--muted);
  line-height: 1.5;
}

/* ALGORITHMS */
.algo-section {
  background: var(--ink);
  color: var(--paper);
}
.algo-section .section-title { color: var(--paper); }
.algo-section .section-label { color: var(--gold); }
.algo-section .section-label::before { background: var(--gold); }
.algo-inner { max-width: 1200px; margin: 0 auto; }
.algo-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1.5px;
  margin-top: 4rem;
  background: rgba(255,255,255,0.05);
}
.algo-card {
  background: var(--ink);
  padding: 2.5rem 2rem;
  position: relative;
  overflow: hidden;
  transition: background 0.3s;
}
.algo-card::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 3px;
  transition: transform 0.3s;
  transform: scaleX(0);
  transform-origin: left;
}
.svm-card::before { background: var(--accent); }
.dt-card::before  { background: var(--gold); }
.knn-card::before { background: var(--accent2); }
.nb-card::before  { background: #2a9d4c; }
.algo-card:hover::before { transform: scaleX(1); }
.algo-card:hover { background: rgba(255,255,255,0.03); }

.algo-abbr {
  font-family: 'Fraunces', serif;
  font-size: 3rem;
  font-weight: 700;
  margin-bottom: 1rem;
  line-height: 1;
}
.svm-card .algo-abbr { color: var(--accent); }
.dt-card  .algo-abbr { color: var(--gold); }
.knn-card .algo-abbr { color: var(--accent2); }
.nb-card  .algo-abbr { color: #2a9d4c; }

.algo-name {
  font-family: 'Syne', sans-serif;
  font-size: 0.8rem;
  font-weight: 700;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  color: rgba(255,255,255,0.6);
  margin-bottom: 1rem;
}
.algo-desc {
  font-size: 0.8rem;
  line-height: 1.8;
  color: rgba(255,255,255,0.4);
  margin-bottom: 2rem;
}
.algo-score-label {
  font-size: 0.65rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: rgba(255,255,255,0.3);
  margin-bottom: 0.5rem;
}
.algo-score-bar {
  height: 3px;
  background: rgba(255,255,255,0.08);
  border-radius: 2px;
  overflow: hidden;
  margin-bottom: 0.4rem;
}
.algo-score-fill {
  height: 100%;
  border-radius: 2px;
  width: 0;
  transition: width 1.2s cubic-bezier(0.25, 1, 0.5, 1);
}
.svm-card .algo-score-fill { background: var(--accent); }
.dt-card  .algo-score-fill { background: var(--gold); }
.knn-card .algo-score-fill { background: var(--accent2); }
.nb-card  .algo-score-fill { background: #2a9d4c; }
.algo-pct {
  font-family: 'Fraunces', serif;
  font-size: 1rem;
  font-weight: 700;
}

/* RESULTS TABLE */
.results-section { background: var(--cream); }
.results-inner { max-width: 1200px; margin: 0 auto; }
.results-tabs {
  display: flex;
  gap: 0;
  margin-top: 3rem;
  border-bottom: 2px solid var(--border);
}
.tab-btn {
  padding: 0.8rem 1.5rem;
  font-family: 'DM Mono', monospace;
  font-size: 0.75rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  background: none;
  border: none;
  cursor: none;
  color: var(--muted);
  border-bottom: 2px solid transparent;
  margin-bottom: -2px;
  transition: all 0.2s;
}
.tab-btn.active { color: var(--accent); border-bottom-color: var(--accent); }
.tab-content { display: none; padding-top: 2rem; }
.tab-content.active { display: block; }
.results-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.82rem;
}
.results-table th {
  font-family: 'Syne', sans-serif;
  font-size: 0.7rem;
  font-weight: 700;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  text-align: left;
  padding: 1rem 1.5rem;
  background: var(--paper);
  border-bottom: 2px solid var(--border);
  color: var(--muted);
}
.results-table td {
  padding: 1rem 1.5rem;
  border-bottom: 1px solid var(--border);
  color: var(--ink);
}
.results-table tr:hover td { background: rgba(200, 75, 30, 0.03); }
.badge-best {
  font-size: 0.6rem;
  background: var(--accent);
  color: white;
  padding: 0.2rem 0.5rem;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  margin-left: 0.5rem;
  vertical-align: middle;
}
.acc-bar {
  display: flex;
  align-items: center;
  gap: 0.8rem;
}
.acc-track {
  width: 100px;
  height: 3px;
  background: var(--border);
  border-radius: 2px;
  overflow: hidden;
}
.acc-fill {
  height: 100%;
  background: var(--accent);
  border-radius: 2px;
}
.improvement { color: #2a9d4c; font-size: 0.8rem; }

/* FEATURES */
.features-section { background: var(--paper); }
.features-inner { max-width: 1200px; margin: 0 auto; }
.features-grid {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 1px;
  margin-top: 4rem;
  background: var(--border);
}
.feat-card {
  background: var(--paper);
  padding: 2rem 1.5rem;
  transition: all 0.3s;
  position: relative;
}
.feat-card:hover { background: var(--ink); }
.feat-card:hover .feat-name,
.feat-card:hover .feat-label { color: white; }
.feat-card:hover .feat-rank { border-color: var(--accent); color: var(--accent); }
.feat-card:hover .feat-desc { color: rgba(255,255,255,0.4); }
.feat-rank {
  width: 2rem; height: 2rem;
  border: 1.5px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.7rem;
  margin-bottom: 1.5rem;
  transition: all 0.3s;
}
.feat-name {
  font-family: 'Syne', sans-serif;
  font-size: 0.85rem;
  font-weight: 700;
  margin-bottom: 0.5rem;
  transition: color 0.3s;
}
.feat-label {
  font-size: 0.7rem;
  letter-spacing: 0.05em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 0.8rem;
  transition: color 0.3s;
}
.feat-importance {
  font-family: 'Fraunces', serif;
  font-size: 1.6rem;
  font-weight: 700;
  color: var(--accent);
  line-height: 1;
  margin-bottom: 0.5rem;
}
.feat-desc {
  font-size: 0.72rem;
  color: var(--muted);
  line-height: 1.6;
  transition: color 0.3s;
}

/* CLUSTER */
.cluster-section {
  background: var(--cream);
  border-top: 1px solid var(--border);
}
.cluster-inner { max-width: 1200px; margin: 0 auto; }
.cluster-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
  margin-top: 4rem;
}
.cluster-card {
  border: 1.5px solid var(--border);
  padding: 2.5rem 2rem;
  background: var(--card);
  position: relative;
  transition: transform 0.3s;
}
.cluster-card:hover { transform: translateY(-5px); }
.cluster-grade {
  font-family: 'Fraunces', serif;
  font-size: 4rem;
  font-weight: 700;
  line-height: 1;
  margin-bottom: 0.5rem;
}
.grade-a { color: var(--accent2); }
.grade-b { color: var(--accent); }
.grade-c { color: var(--gold); }
.cluster-label {
  font-family: 'Syne', sans-serif;
  font-size: 0.7rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  margin-bottom: 1.5rem;
}
.cluster-detail {
  font-size: 0.8rem;
  line-height: 1.8;
  color: var(--muted);
}
.cluster-detail strong { color: var(--ink); }
.cluster-tag {
  position: absolute;
  top: 1.5rem; right: 1.5rem;
  font-size: 0.65rem;
  padding: 0.3rem 0.7rem;
  letter-spacing: 0.05em;
}
.tag-a { background: var(--accent2); color: white; }
.tag-b { background: var(--accent); color: white; }
.tag-c { background: var(--gold); color: white; }

/* PREDICTOR */
.predictor-section {
  background: var(--ink);
  color: var(--paper);
  position: relative;
  overflow: hidden;
}
.predictor-section::before {
  content: '';
  position: absolute;
  inset: 0;
  background-image: linear-gradient(rgba(255,255,255,0.02) 1px, transparent 1px),
                    linear-gradient(90deg, rgba(255,255,255,0.02) 1px, transparent 1px);
  background-size: 60px 60px;
}
.predictor-inner {
  max-width: 1200px;
  margin: 0 auto;
  position: relative;
  z-index: 1;
}
.predictor-section .section-title { color: var(--paper); }
.predictor-section .section-label { color: var(--gold); }
.predictor-section .section-label::before { background: var(--gold); }
.predictor-layout {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 5rem;
  margin-top: 4rem;
  align-items: start;
}
.form-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1.5rem;
}
.form-group { display: flex; flex-direction: column; gap: 0.5rem; }
.form-group.full { grid-column: 1 / -1; }
.form-label {
  font-size: 0.65rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: rgba(255,255,255,0.4);
}
.form-control {
  background: rgba(255,255,255,0.04);
  border: 1px solid rgba(255,255,255,0.08);
  color: var(--paper);
  padding: 0.85rem 1rem;
  font-family: 'DM Mono', monospace;
  font-size: 0.82rem;
  outline: none;
  transition: border-color 0.2s, background 0.2s;
  appearance: none;
  cursor: none;
}
.form-control:focus {
  border-color: rgba(200,75,30,0.6);
  background: rgba(255,255,255,0.07);
}
.form-control option { background: #1a1a22; color: var(--paper); }
.predict-btn {
  margin-top: 2rem;
  width: 100%;
  padding: 1rem;
  background: var(--accent);
  color: white;
  font-family: 'Syne', sans-serif;
  font-size: 0.85rem;
  font-weight: 700;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  border: none;
  cursor: none;
  transition: all 0.2s;
}
.predict-btn:hover { background: #a83b14; transform: translateY(-2px); }

.result-panel {
  background: rgba(255,255,255,0.03);
  border: 1px solid rgba(255,255,255,0.08);
  padding: 2.5rem;
  min-height: 300px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  position: relative;
  overflow: hidden;
}
.result-idle {
  color: rgba(255,255,255,0.2);
  font-size: 0.8rem;
  line-height: 2;
}
.result-output { display: none; }
.result-output.show { display: block; }
.result-verdict {
  font-family: 'Fraunces', serif;
  font-size: 3.5rem;
  font-weight: 700;
  line-height: 1;
  margin-bottom: 0.5rem;
}
.verdict-pass { color: #4ade80; }
.verdict-fail { color: var(--accent); }
.verdict-distinction { color: var(--gold); }
.verdict-withdrawn { color: rgba(255,255,255,0.5); }
.result-conf {
  font-size: 0.8rem;
  color: rgba(255,255,255,0.4);
  margin-bottom: 2rem;
}
.result-breakdown {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 0.8rem;
  text-align: left;
}
.breakdown-row {
  display: flex;
  align-items: center;
  gap: 1rem;
  font-size: 0.75rem;
}
.breakdown-label {
  width: 80px;
  color: rgba(255,255,255,0.4);
  flex-shrink: 0;
  font-size: 0.7rem;
}
.breakdown-bar {
  flex: 1;
  height: 3px;
  background: rgba(255,255,255,0.06);
  border-radius: 2px;
  overflow: hidden;
}
.breakdown-fill {
  height: 100%;
  border-radius: 2px;
  transition: width 1s ease;
}
.breakdown-pct {
  width: 35px;
  text-align: right;
  color: rgba(255,255,255,0.5);
  font-size: 0.7rem;
}

/* MODULES */
.modules-section { background: var(--paper); }
.modules-inner { max-width: 1200px; margin: 0 auto; }
.modules-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.5px;
  margin-top: 4rem;
  background: var(--border);
}
.module-card {
  background: var(--paper);
  padding: 2rem;
  transition: background 0.3s;
}
.module-card:hover { background: var(--cream); }
.module-file {
  font-size: 0.7rem;
  color: var(--accent);
  letter-spacing: 0.05em;
  margin-bottom: 1rem;
  font-weight: 500;
}
.module-name {
  font-family: 'Syne', sans-serif;
  font-size: 1rem;
  font-weight: 800;
  margin-bottom: 0.5rem;
  letter-spacing: -0.01em;
}
.module-role {
  font-size: 0.78rem;
  color: var(--muted);
  margin-bottom: 1.2rem;
  line-height: 1.6;
}
.module-fns {
  display: flex;
  flex-direction: column;
  gap: 0.3rem;
}
.fn-tag {
  font-size: 0.68rem;
  color: var(--muted);
  padding: 0.25rem 0.6rem;
  background: var(--cream);
  display: inline-block;
  margin-right: 0.3rem;
  margin-bottom: 0.3rem;
}

/* REQUIREMENTS */
.req-section { background: var(--cream); }
.req-inner { max-width: 1200px; margin: 0 auto; }
.req-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  margin-top: 4rem;
}
.req-table-title {
  font-family: 'Syne', sans-serif;
  font-size: 0.75rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  margin-bottom: 1.5rem;
  color: var(--muted);
}
.req-table {
  width: 100%;
  border-collapse: collapse;
  font-size: 0.8rem;
}
.req-table td {
  padding: 0.8rem 1rem;
  border-bottom: 1px solid var(--border);
  vertical-align: top;
  line-height: 1.6;
}
.req-table td:first-child {
  font-weight: 500;
  color: var(--muted);
  width: 40%;
  font-size: 0.75rem;
  text-transform: uppercase;
  letter-spacing: 0.03em;
}

/* FOOTER */
footer {
  background: var(--ink);
  color: var(--paper);
  padding: 4rem 3rem 3rem;
}
.footer-inner {
  max-width: 1200px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 2fr 1fr 1fr 1fr;
  gap: 3rem;
}
.footer-brand {
  font-family: 'Syne', sans-serif;
  font-size: 1.2rem;
  font-weight: 800;
  margin-bottom: 1rem;
}
.footer-brand span { color: var(--accent); }
.footer-desc {
  font-size: 0.78rem;
  color: rgba(255,255,255,0.3);
  line-height: 1.8;
}
.footer-col-title {
  font-size: 0.65rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: rgba(255,255,255,0.3);
  margin-bottom: 1.2rem;
}
.footer-links {
  list-style: none;
  display: flex;
  flex-direction: column;
  gap: 0.6rem;
}
.footer-links a {
  font-size: 0.8rem;
  color: rgba(255,255,255,0.5);
  text-decoration: none;
  transition: color 0.2s;
}
.footer-links a:hover { color: var(--paper); }
.footer-bottom {
  max-width: 1200px;
  margin: 3rem auto 0;
  padding-top: 2rem;
  border-top: 1px solid rgba(255,255,255,0.06);
  display: flex;
  justify-content: space-between;
  font-size: 0.72rem;
  color: rgba(255,255,255,0.2);
}

/* SCROLL REVEAL */
.reveal {
  opacity: 0;
  transform: translateY(30px);
  transition: opacity 0.7s ease, transform 0.7s ease;
}
.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}

/* RESPONSIVE */
@media (max-width: 900px) {
  .hero { grid-template-columns: 1fr; }
  .hero-right { display: none; }
  .abstract-grid { grid-template-columns: 1fr; gap: 2rem; }
  .algo-grid { grid-template-columns: repeat(2, 1fr); }
  .features-grid { grid-template-columns: repeat(2, 1fr); }
  .cluster-grid { grid-template-columns: 1fr; }
  .predictor-layout { grid-template-columns: 1fr; gap: 3rem; }
  .modules-grid { grid-template-columns: 1fr; }
  .req-grid { grid-template-columns: 1fr; }
  .footer-inner { grid-template-columns: 1fr 1fr; }
  .pipeline-steps { grid-template-columns: repeat(4, 1fr); }
  nav { padding: 1rem 1.5rem; }
  section { padding: 4rem 1.5rem; }
}
</style>
</head>
<body>

<!-- Cursor -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- NAV -->
<nav>
  <div class="nav-logo">Student<span>IQ</span></div>
  <ul class="nav-links">
    <li><a href="#abstract">Abstract</a></li>
    <li><a href="#pipeline">Pipeline</a></li>
    <li><a href="#algorithms">Models</a></li>
    <li><a href="#results">Results</a></li>
    <li><a href="#predictor">Demo</a></li>
  </ul>
  <div class="nav-badge">B.Tech CSE · 2025–26</div>
</nav>

<!-- HERO -->
<section class="hero" style="padding:0;">
  <div class="hero-left">
    <div class="hero-tag">Educational Data Mining · ML Research</div>
    <h1 class="hero-title">Student<br><em>Performance</em><br>Prediction</h1>
    <p class="hero-desc">A full machine learning pipeline for predicting academic outcomes using SVM, Decision Tree, KNN, and Naive Bayes. Replication of Ahmed (2024) — Applied Computational Intelligence.</p>
    <div class="hero-buttons">
      <a href="#predictor" class="btn-primary">Try Live Demo</a>
      <a href="#pipeline" class="btn-secondary">View Pipeline</a>
    </div>
    <div class="hero-stats">
      <div class="stat-item">
        <div class="stat-number">96.0%</div>
        <div class="stat-label">SVM Accuracy</div>
      </div>
      <div class="stat-item">
        <div class="stat-number">32,005</div>
        <div class="stat-label">Students</div>
      </div>
      <div class="stat-item">
        <div class="stat-number">4</div>
        <div class="stat-label">ML Models</div>
      </div>
    </div>
  </div>
  <div class="hero-right">
    <div class="hero-grid-bg"></div>
    <div class="hero-visual">
      <div class="model-cards">
        <div class="model-card">
          <div class="model-icon" style="background:rgba(200,75,30,0.15); color:#c84b1e;">⚙</div>
          <div class="model-info">
            <div class="model-name">Support Vector Machine</div>
            <div class="model-sub">RBF Kernel · C=10 · γ=0.01</div>
          </div>
          <div class="model-acc" style="color:#c84b1e;">96.0%</div>
        </div>
        <div class="model-card">
          <div class="model-icon" style="background:rgba(196,146,42,0.15); color:#c4922a;">🌿</div>
          <div class="model-info">
            <div class="model-name">Decision Tree</div>
            <div class="model-sub">Max Depth=7 · Min Split=2</div>
          </div>
          <div class="model-acc" style="color:#c4922a;">93.4%</div>
        </div>
        <div class="model-card">
          <div class="model-icon" style="background:rgba(30,95,200,0.15); color:#1e5fc8;">◎</div>
          <div class="model-info">
            <div class="model-name">K-Nearest Neighbors</div>
            <div class="model-sub">k=8 · Weight=Distance</div>
          </div>
          <div class="model-acc" style="color:#1e5fc8;">87.4%</div>
        </div>
        <div class="model-card">
          <div class="model-icon" style="background:rgba(42,157,76,0.15); color:#2a9d4c;">∼</div>
          <div class="model-info">
            <div class="model-name">Naive Bayes</div>
            <div class="model-sub">Var Smoothing=1e-9</div>
          </div>
          <div class="model-acc" style="color:#2a9d4c;">83.3%</div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- ABSTRACT -->
<section class="abstract-section" id="abstract">
  <div class="abstract-grid">
    <div>
      <div class="section-label">Overview</div>
      <h2 class="section-title">Project<br><em>Abstract</em></h2>
    </div>
    <div>
      <div class="abstract-text">
        <p>This project presents a comprehensive replication and extension of the research by Esmael Ahmed (2024), published in <em>Applied Computational Intelligence and Soft Computing</em>. The study applies Educational Data Mining (EDM) techniques to predict student academic outcomes using a dataset of <strong>32,005 students</strong> from Wollo University and the Kombolcha Institute of Technology.</p>
        <p>The proposed system follows a multi-stage pipeline: data collection from the A+ Learning Management System, rigorous preprocessing, feature selection via Random Forest under 5-fold cross-validation, K-Means clustering using the Elbow Method, and supervised classification with four algorithms — SVM, DT, KNN, and Naive Bayes.</p>
        <p>Hyperparameter optimization via Grid Search with 10-fold cross-validation achieved a peak accuracy of <strong>96.0% (SVM–RBF)</strong>. Key predictive features: entrance result, number of previous attempts, studied credits, gender, and region.</p>
        <div class="keyword-list">
          <span class="keyword">Machine Learning</span>
          <span class="keyword">EDM</span>
          <span class="keyword">SVM</span>
          <span class="keyword">K-Means</span>
          <span class="keyword">Grid Search</span>
          <span class="keyword">Decision Tree</span>
          <span class="keyword">KNN</span>
          <span class="keyword">Naive Bayes</span>
          <span class="keyword">Scikit-learn</span>
          <span class="keyword">Python</span>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- PIPELINE -->
<section class="pipeline-section" id="pipeline">
  <div class="inner">
    <div class="section-label">Architecture</div>
    <h2 class="section-title">ML <em>Pipeline</em></h2>
    <div class="pipeline-steps">
      <div class="pipe-step">
        <div class="pipe-num">01</div>
        <div class="pipe-title">Data<br>Collection</div>
        <div class="pipe-sub">A+ LMS export · 32,582 raw records</div>
      </div>
      <div class="pipe-step">
        <div class="pipe-num">02</div>
        <div class="pipe-title">Data<br>Cleaning</div>
        <div class="pipe-sub">Remove nulls & duplicates · 577 removed</div>
      </div>
      <div class="pipe-step">
        <div class="pipe-num">03</div>
        <div class="pipe-title">Encoding &amp;<br>Scaling</div>
        <div class="pipe-sub">Label encode · Ordinal encode · StandardScaler</div>
      </div>
      <div class="pipe-step">
        <div class="pipe-num">04</div>
        <div class="pipe-title">Feature<br>Selection</div>
        <div class="pipe-sub">Random Forest · 5-fold CV · Top-5 features</div>
      </div>
      <div class="pipe-step">
        <div class="pipe-num">05</div>
        <div class="pipe-title">K-Means<br>Clustering</div>
        <div class="pipe-sub">Elbow Method · K=3 · Grades A/B/C</div>
      </div>
      <div class="pipe-step">
        <div class="pipe-num">06</div>
        <div class="pipe-title">Model<br>Training</div>
        <div class="pipe-sub">SVM, DT, KNN, NB · 80/20 stratified split</div>
      </div>
      <div class="pipe-step">
        <div class="pipe-num">07</div>
        <div class="pipe-title">HPO &amp;<br>Evaluation</div>
        <div class="pipe-sub">Grid Search · 10-fold CV · Kappa · Accuracy</div>
      </div>
    </div>
  </div>
</section>

<!-- ALGORITHMS -->
<section class="algo-section" id="algorithms">
  <div class="algo-inner">
    <div class="section-label">Classification</div>
    <h2 class="section-title">Four <em>Algorithms</em></h2>
    <div class="algo-grid">
      <div class="algo-card svm-card">
        <div class="algo-abbr">SVM</div>
        <div class="algo-name">Support Vector Machine</div>
        <div class="algo-desc">Maximizes the margin between class boundaries in high-dimensional feature space. The RBF kernel enables non-linear classification, making it ideal for correlated student data.</div>
        <div class="algo-score-label">Post-tuning accuracy</div>
        <div class="algo-score-bar"><div class="algo-score-fill" data-width="96.03"></div></div>
        <div class="algo-pct" style="color:var(--accent);">96.03%</div>
      </div>
      <div class="algo-card dt-card">
        <div class="algo-abbr">DT</div>
        <div class="algo-name">Decision Tree</div>
        <div class="algo-desc">Hierarchical rule-based classifier using Gini impurity splits. Highly interpretable — decision paths can be visualized and communicated to academic counselors directly.</div>
        <div class="algo-score-label">Post-tuning accuracy</div>
        <div class="algo-score-bar"><div class="algo-score-fill" data-width="93.41"></div></div>
        <div class="algo-pct" style="color:var(--gold);">93.41%</div>
      </div>
      <div class="algo-card knn-card">
        <div class="algo-abbr">KNN</div>
        <div class="algo-name">K-Nearest Neighbors</div>
        <div class="algo-desc">Instance-based learner classifying a student by similarity to its k=8 nearest neighbors in feature space. Distance-weighted voting improves accuracy at cluster boundaries.</div>
        <div class="algo-score-label">Post-tuning accuracy</div>
        <div class="algo-score-bar"><div class="algo-score-fill" data-width="87.38"></div></div>
     
