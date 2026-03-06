import { useState, useEffect } from "react";

// ─── DESIGN SYSTEM ──────────────────────────────────────────────────────────
const COLORS = {
  forest: "#1a4a2e",
  sage: "#3a7d5c",
  mint: "#6dbf8e",
  cream: "#f5f0e8",
  sand: "#e8dfc8",
  charcoal: "#1c1c1e",
  mist: "#f0f4f1",
  gold: "#c8a84b",
};

const globalStyles = `
  @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;600;700&family=DM+Sans:wght@300;400;500;600&display=swap');

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --forest: #1a4a2e;
    --sage: #3a7d5c;
    --mint: #6dbf8e;
    --cream: #f5f0e8;
    --sand: #e8dfc8;
    --charcoal: #1c1c1e;
    --mist: #f0f4f1;
    --gold: #c8a84b;
  }

  body { font-family: 'DM Sans', sans-serif; background: var(--cream); color: var(--charcoal); overflow-x: hidden; }

  .font-display { font-family: 'Playfair Display', serif; }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(28px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }
  @keyframes float {
    0%, 100% { transform: translateY(0px); }
    50% { transform: translateY(-10px); }
  }
  @keyframes leafSpin {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }
  @keyframes shimmer {
    0% { background-position: -200% center; }
    100% { background-position: 200% center; }
  }
  @keyframes slideIn {
    from { opacity: 0; transform: translateX(-16px); }
    to { opacity: 1; transform: translateX(0); }
  }
  @keyframes pulse {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.5; }
  }

  .animate-fadeUp { animation: fadeUp 0.7s ease forwards; }
  .animate-float { animation: float 4s ease-in-out infinite; }
  .animate-fadeIn { animation: fadeIn 0.5s ease forwards; }
  .animate-slideIn { animation: slideIn 0.4s ease forwards; }

  .delay-100 { animation-delay: 0.1s; }
  .delay-200 { animation-delay: 0.2s; }
  .delay-300 { animation-delay: 0.3s; }
  .delay-400 { animation-delay: 0.4s; }
  .delay-500 { animation-delay: 0.5s; }

  .btn-primary {
    background: var(--forest);
    color: var(--cream);
    border: none;
    padding: 14px 32px;
    border-radius: 50px;
    font-family: 'DM Sans', sans-serif;
    font-size: 15px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.25s ease;
    letter-spacing: 0.3px;
  }
  .btn-primary:hover { background: var(--sage); transform: translateY(-2px); box-shadow: 0 8px 24px rgba(26,74,46,0.25); }

  .btn-outline {
    background: transparent;
    color: var(--forest);
    border: 2px solid var(--forest);
    padding: 12px 28px;
    border-radius: 50px;
    font-family: 'DM Sans', sans-serif;
    font-size: 15px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.25s ease;
  }
  .btn-outline:hover { background: var(--forest); color: var(--cream); transform: translateY(-2px); }

  .btn-ghost {
    background: transparent;
    color: var(--charcoal);
    border: none;
    padding: 10px 20px;
    font-family: 'DM Sans', sans-serif;
    font-size: 14px;
    font-weight: 500;
    cursor: pointer;
    transition: color 0.2s;
  }
  .btn-ghost:hover { color: var(--sage); }

  .card {
    background: white;
    border-radius: 20px;
    box-shadow: 0 4px 24px rgba(26,74,46,0.08);
    transition: all 0.3s ease;
  }
  .card:hover { transform: translateY(-4px); box-shadow: 0 12px 40px rgba(26,74,46,0.14); }

  .input-field {
    width: 100%;
    padding: 14px 18px;
    border: 2px solid var(--sand);
    border-radius: 12px;
    font-family: 'DM Sans', sans-serif;
    font-size: 15px;
    background: white;
    color: var(--charcoal);
    outline: none;
    transition: border-color 0.2s;
  }
  .input-field:focus { border-color: var(--sage); }
  .input-field::placeholder { color: #aab0a8; }

  select.input-field { appearance: none; }

  .label { display: block; font-size: 13px; font-weight: 600; color: var(--forest); margin-bottom: 6px; letter-spacing: 0.3px; text-transform: uppercase; }

  .tag {
    display: inline-block;
    padding: 5px 14px;
    border-radius: 50px;
    font-size: 12px;
    font-weight: 600;
    letter-spacing: 0.4px;
  }

  .progress-bar { height: 4px; background: var(--sand); border-radius: 2px; overflow: hidden; }
  .progress-fill { height: 100%; background: linear-gradient(90deg, var(--sage), var(--mint)); border-radius: 2px; transition: width 0.4s ease; }

  .mesh-bg {
    background:
      radial-gradient(ellipse at 20% 20%, rgba(109,191,142,0.18) 0%, transparent 50%),
      radial-gradient(ellipse at 80% 80%, rgba(26,74,46,0.12) 0%, transparent 50%),
      radial-gradient(ellipse at 60% 10%, rgba(200,168,75,0.08) 0%, transparent 40%),
      var(--cream);
  }

  .noise-overlay {
    position: relative;
  }
  .noise-overlay::after {
    content: '';
    position: absolute;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.03'/%3E%3C/svg%3E");
    pointer-events: none;
    border-radius: inherit;
  }

  /* Scrollbar */
  ::-webkit-scrollbar { width: 6px; }
  ::-webkit-scrollbar-track { background: var(--cream); }
  ::-webkit-scrollbar-thumb { background: var(--sage); border-radius: 3px; }
`;

// ─── SVG ICONS ───────────────────────────────────────────────────────────────
const LeafIcon = ({ size = 24, color = "currentColor" }) => (
  <svg width={size} height={size} viewBox="0 0 24 24" fill="none" stroke={color} strokeWidth="2" strokeLinecap="round" strokeLinejoin="round">
    <path d="M11 20A7 7 0 0 1 9.8 6.1C15.5 5 17 4.48 19 2c1 2 2 4.18 2 8 0 5.5-4.78 10-10 10z"/>
    <path d="M2 21c0-3 1.85-5.36 5.08-6C9.5 14.52 12 13 13 12"/>
  </svg>
);

const HandshakeIcon = ({ size = 24, color = "currentColor" }) => (
  <svg width={size} height={size} viewBox="0 0 24 24" fill="none" stroke={color} strokeWidth="2" strokeLinecap="round" strokeLinejoin="round">
    <path d="m11 17 2 2a1 1 0 1 0 3-3"/>
    <path d="m14 14 2.5 2.5a1 1 0 1 0 3-3l-3.88-3.88a3 3 0 0 0-4.24 0l-.88.88a1 1 0 1 1-3-3l2.81-2.81a5.79 5.79 0 0 1 7.06-.87l.47.28a2 2 0 0 0 1.42.25L21 4"/>
    <path d="m21 3 1 11h-2"/>
    <path d="M3 3 2 14l6.5 6.5a1 1 0 1 0 3-3"/>
    <path d="M3 4h8"/>
  </svg>
);

const UsersIcon = ({ size = 24, color = "currentColor" }) => (
  <svg width={size} height={size} viewBox="0 0 24 24" fill="none" stroke={color} strokeWidth="2" strokeLinecap="round" strokeLinejoin="round">
    <path d="M16 21v-2a4 4 0 0 0-4-4H6a4 4 0 0 0-4 4v2"/>
    <circle cx="9" cy="7" r="4"/>
    <path d="M22 21v-2a4 4 0 0 0-3-3.87"/>
    <path d="M16 3.13a4 4 0 0 1 0 7.75"/>
  </svg>
);

const StarIcon = ({ size = 24, color = "currentColor" }) => (
  <svg width={size} height={size} viewBox="0 0 24 24" fill="none" stroke={color} strokeWidth="2" strokeLinecap="round" strokeLinejoin="round">
    <polygon points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2"/>
  </svg>
);

const MapPinIcon = ({ size = 20, color = "currentColor" }) => (
  <svg width={size} height={size} viewBox="0 0 24 24" fill="none" stroke={color} strokeWidth="2" strokeLinecap="round" strokeLinejoin="round">
    <path d="M20 10c0 6-8 12-8 12s-8-6-8-12a8 8 0 0 1 16 0Z"/>
    <circle cx="12" cy="10" r="3"/>
  </svg>
);

const CheckIcon = ({ size = 18, color = "currentColor" }) => (
  <svg width={size} height={size} viewBox="0 0 24 24" fill="none" stroke={color} strokeWidth="2.5" strokeLinecap="round" strokeLinejoin="round">
    <polyline points="20 6 9 17 4 12"/>
  </svg>
);

const ArrowRightIcon = ({ size = 18, color = "currentColor" }) => (
  <svg width={size} height={size} viewBox="0 0 24 24" fill="none" stroke={color} strokeWidth="2" strokeLinecap="round" strokeLinejoin="round">
    <path d="M5 12h14"/><path d="m12 5 7 7-7 7"/>
  </svg>
);

const LA_GRAINE_LOGO = "data:image/jpeg;base64,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FHD+7JJNNs0AGfap6KAI/LHmdakoooAKKKKACiiigAooooAKKKKACiiigAooooAKKKKACiiigAooooAb5fvTSMjFFFAD2Py5BpsJ4psRAIBNKmAcA96S2Akopo/epzRGMLimA6iiigAooooAXe3rRk+ppKKACiiigAooooAKKKKACiiigAooooAKKTevrS0AFFFN8z2oAdRRkYzURiMhz5Xb0oAMr6/rRFhMZy30NJ9n/wBn9aNOi/1hHagCaiiigAooII6iigAooooAKKKKACiiigBxhmC7vMH502iigAooooAKKKKACiik2D1NAAn3RS0idPxpaACiiigAoGc8UUAkHIoAcr9iaMf9NKbQOvXFABRShS3U0u0/3RQAgAJ5NJTgh70BdpyWoAaM54pzbvwpwxjiigTdhhDDrSVIQD1FMIx3zQMSiiigAooooARpc9qWo6fvHoaAE8pfU/nVWrbnC1WVd3zNQA0DPAqaA/KPrTAoHSjYw5U0AWaRmC0kU3bgUjnLUAG4Yxtpy4xxUe8A4NIAyjOEbvxQBMCDyKjY89e9JGN46YqWgCOmOzcnBH4VPSFQRignmIMHdnHfmrKg4JjweaSpEBYUGctyHy/U0sQGMZpaSOMxHnrQbBsHqaWiigAooooAKKKKACgEjkUUUAQk5iPApqoxPXP41YqHHknrQAnlt60lSUUAVGUj6VFVt/umqlAElq4jLk98U+yznp1qOPn86sWYAPP4UtAJSQBk1LB/rTUJz+8AHTFTJgEmmZjDtzx+lJvb1ocAHikoAkqOpKYTkk0lsaQIDE0ZxzzSEnzePSlj69KC65/1YpgRM2eB0pLNufLz3p1sMynpQgO4/WgCQRkN1709Sc/zpcLsziiAZB2igzGW8gEz5qeD78n1qK2T5pOKnoCA3yk9KXYPU0tFBoJxjyjSxn9yBSkN1IpKACiiigApcHGcUqnuW/CnZ4yKAGZI4p2wepplOj70AByq43U2nkfLgCo/mWOgBaKKKACiiigAooooAKKCMcGigAooooAKKAQeRQCD0NABRRRQAU2TtTqKAK8ZBPFPi+6tPDeYAijOKSMcP7GgB9FER/cjmigAooooAKKKKACiiigAooooAKKTd/sn8qWgAooooAKKDIW625qNZMnqaDHnJCCDg0HGeKKMnOaDYKihZd2fLNS0UAFN8pPSnUUAN8pfU/nRFNzinUiggYNAEX3m4ai3i8ogkU8QqO5p9ABRRRQAUUUUGZHbnJkLDp0pLdwTwe1OSAkSBe9NtIivUnpQOBLRRRQWFFJsX0paACiigEHkUAFFFFABRRRQAUUVF53Yn9KAJaKbGcinUAFFLbSkYz+tJQAUU4bl/hptAC9uv4U3zfc0tFACQS46VKDkZqpuwx+tWUIx1oAdUJznIzUwIPIpGGRwKAIKntpAvWoKfF/WgCWmldxyDTqKAAAAYFNx/wBNKdTX6/hQA2ipKjoAKKKTYPU0ADj5aIP+PcUtV45DbHI6+tAFik81f7/60tV6DMfbD97Lzxjio4pRjk0EDBqFhGT900GhKPNbjPWnQ5pluAT1pbaIKcgUAWYwdvApaVCFTIpIeIAff+tAAc96KcFyM9zSAAjjrQAlFLg+hpKACiiigAooooAKKKKACiiigAooooAKKKKACo6kqIt/r+OlAEZ5HBqEjDYqf6VGVlznP04oAYAT0qeNsAEelM5zuxTIyehoAsQn/RsHrjpUkQ2/Mp6iookMAyetEBGRQZk21T2o2jO4UtIowMZoAWoTxF93vU1IwHXFBoVASORTpOv4UR96aST1NAEcQ5joT5mOPU1KgyelJaAg8igCaIA223HUGltohEuBRAAQMDpUtBmPjxjn1pu5vWj5/ehQcjjvQAhGDigEg5FLk5zQP880GgpTA4ptObcf4abQAUUUqnBoASneZ7U6o6ADr1NKpwc0lFAD0+6KXAxjFNRieDTqACmvgfw06j60AR0AZ4FABPQUo69cUAAUnpS+Z7UkZ+c49KjIwcCgCbGBgCmdegp/GBmq8Iy3SglsSA4wSKd5g9F6U6VN64xVYwL60Ek+QTwadHnOf61T24zipoQPs/GOtBoTr3+tNh4IpYxhcUh69MUAPppkUHGabUdABHIDyRuPtUwkUjA9KZFFxnNP8sdzQAR56VJH3pkMRzil6UQAKKKKACkhlJPSlpke0d6AH0UUUAFH0oooAM3HqfzpV6jNNf7ppbaHnigzEXGOPWloooNAooooFZBRRRQMKKKKACiiigAoopAcn7tAC0UUUAFIGB70tVMH0NAFuiorLOHzUtABRRRQAifdFLRRQAUU2PzemBUdupDSD2oAlAHdRUUAOQSKf5Xs9PAA6CgAoopluc+Z/nvQA+iiigAqOpKjoAa6/wAWakg27nxTcD0FOi+5QA6iiigByv2Jpp69c0uTjFBJPWgBKKKKAI6Kf5YzyaAgBzQA6E/L170+mYHp+tJQACAdzR5e3jP605WUD0p1ADQpJ+anDHamgqvG6mg4OaAH8Dt0pPM9qQMR0pKAFwv979KSgEjoaKACigAnoKCMcGgCOm/8s6mpI4sHntQA5up+tMc9qewwaFGTigzK1R1YMWOq0IvRTSujQggPBp6HA+Wm7HzlhUsXAApgLAcGpvM9qhi7VJQA5X7E0oRR0FNBI6U8DAxQAj/dNMqQjIxTGXHIoASiinKVA+9QAFP7pppGDipKZk5zQAlFFFACbx6GlqOiEYwKAJKKKKACiiigAooooAYWY8Zo3MO9OKKTnJplBF9bkQky049qgo/iJB6mplBJ3GktiyJB8x96faEsfK96RocpknmlAA4FMC2PlXmlBB5FMhJEHFKnXFBmOpG6dM1Eck96dGDjoetBoNc88E00uM8N+tLkdxTPNH/PIVl7QzIouCRUkI2mmjr0/GkhzknHetKZb2LNjgb8GpabD9z8adTICiiig0CiilXqPrQAu7b8uKJO1DKc7qPue+aAG0UuTnNICR0NAACQcijr1NFFABQCQciilBAPIoAQdeuKcr9iaaM9qdtf+9+tAtBpJPU0U7+H71NoGFAODkUUUAEP32pPMHSkOGbG6lCgdKAHZPqaiibnr3pxy4+7TqAFQny8571B5T+lOqSgCvg5xiliHJOKliQx9WzTqACgY70UUARLGCfm+WpaCCODRQAUUUUAKCR0pKKKACiiigCEzAdzRbHLSGidcE0tsvEhoAlooooAKjqSk2D1NAC0UUUAFFFFABRRRQAUU6PvTSQOpoAKKZaE+UcmoViOQc0GZZpkmTDkCn+UM58yigCtEWCP9au0yGPPzEJ+VL5ntQA2iiigAop21P73602gAooooAKKKKACiiigApCSTwfrT/L96jIIHA70ASlsdRTPOA4Apnzf3v1pKAF8/wD3/wAqVZQB0PvxS7VxjFLQAUUUUAK3U/Wko+tFBoFFFRwgjA29uaAJKKKKACiiggjqKACiiigAooooAASDkUUUZI6GgB0fenU1D2p1AERUE5IpacydwKbQAUUUUAFFFFADkPahtv40i9emaeAAMCgCOinMvotNoAKZbYzTkXjn+dRhQvSk9gLHB75qM/eFPQEIfpUa58vn0osgBwOtQ1KEIXr2phH7vBpgO80dOPypFIMY+bvULDBxUsPQFl7UATAkciikhzPH15p0X/Hv+NACRMcfjTmYEU0HBzRQApOTmkBI6GiigBd7etG5j3pKKACiiigApE+6Kdg+ho2N6UAIMd6XqeBSqoK/Whdw/hoAQgjqKSnNuP8ADTSCDg0CWwUUUUDCoS3+sP5VMTjk0yWI5zQZlOUd1XvSwk7OtOooNBFJyfrS0U3TxnigCzb/AOrNTxgAUkahBx3NOAA6UGZBnjNPBPQikMSmpHHI4pXQEBHHU0ynt+P4UyjQFuN3n0FFt++Zxim06xx5sefWmaFm1P7k/SloGe9FBmFFFFBoFKCAeRSUuTnNADmbHAplHXqaASDkUAFFKST1pKACiiigABIORRRSgE9KAF3fL705eg+lFBOBmgVkNQgcE01P85pTnAzTRgDANAxPM9qdSB1Peo8Sg7Q1AC0VIBhAaROBz60CSsPtiSpFNpcn1NJ16mgYUoYjoaTBHUUUAAx3pQGxkCkoGM80AKvBz6Uvme1Bf+6KaSScmgB+8ehplFFABRRRQAUUUUAJsHqaWiigAooooAKKKKACilwfQ0lABRRSbxnGDQAtFFFABSBg1LUIXyj9e1AE1Q+aVOPK/GpI87eadQBD5Hl8CniJcZ9afRQAnlp6mjy09TS0UAFFFBOBk0AFFM85aZvGc7aAJS2Dik3nOMDrUZLMPu0ofBGQc0roCWikU5GTS0zMKKeGGAM0u/8A2v1oAjooooAMg9DTBIe/8qWMGpf4Pwqb20NCrFjMvNCfeFK6bqfBFg55NPRoB9FFFMzCiiigAo6UU/Ce350AM+1beSv60QkFnPvUdPjkiUe/egBaKBz0owT2P5UAFKSNuB+NAVjzikII60AFFKQ2elGD6Gg0EooooAKKKKAHIO9Opv8AufjSK2ODQAP940lFFABRRUFt956AJh+7hc9scUyDvShiYj9acgAXigB8fenUxTg0qt/s/lQA7A9BTfue+adRk+hoAjPXrmijpShSelACx96dSKu0c0jFgfvUAIAWNIQcZxSx8ZJpYpRnHtQBVohG44PrUhGDg02IdgKAHH9yQIm471JDKCev1qOnwY3tigB455C/rSNnPNKuR1BoVWB9KAG0U5wetNoAUKSMgUlEJ+ZhRQAoUnpRtY9qIQNufengADAoAaqsOaUAgcmlowPQUAFFI/T8aRM0AHzbs7aRhg4p69B9KY/3jQAlFFFADXyByaQH1PalZ+wNQ7cRcdaV9LgR0UoHqDSEYODTAKdaA7s4702nIQB170AWqVSd3WkooMxSCOtJSuMNSUABGRiq9WKgf7xoAjix5wz6U+1j7+h61Xhl3TbyOnFXLUZjJ9DWVN3NBxYqcZzSg5GahtjuMtT1qAUUUUAFFFFABRRRQAUUUUAFFFFABSqcNSU6PvQA6g9OmaKbJ2oE9htNf71OoAA6CgY0pgcUi5zxTwABgUUAOTpTiMjFR08MG6igBlFOZTndTR164oAkpirnk0u75fehS3ZaBLYG+VcCm05n7A02gYucH5TSUhYA4NLHNuoAKKKPpQBGv+vNSU2175HalTp+NAC0UUUAFFFFABRUYlz0aiDnpQBJRRRQAuAW/GhSAcmm719aZQZkU+fJ64otJhjBpZsltoqLy2ySDQaExmwOSKSJgYs5qI58st7VLY/xUAPtvu1LSA55xS0lsAUUUUwCiiigAooqmW5wx+tAFyio4zBkHf8ArUyLERkEH6UC5kiAzCNHGOagyD3/AFpbm7tYHceYuFPzc9K8x+KX7XP7PHweLR/EP40aLpkic/ZZb6N5fpsXc1ZVKkUcVXG4bD/FI9Pjx3anAgZye1fHHjv/AILUfsheF90eh6hr2vSKeBpukFFY/wC9KVH6V5V4s/4L2+H0iI8CfAy/nb+B9X1mOMZ91j3GsHiaaPNrZ/gqa+JH6OBjjliOO5xSLNGiNunHXjLV+SPjD/guT+1BrMjDwn4V8K6RGQQN9nNdOo+pYA15vrv/AAVr/bq1mRnh+LFtaIxJ2adpFvHt9vm3GpWMgjy58VYFaJn7bLeRE7d3TjigTxENgDI6H0r8Jbv/AIKZftu3j7n/AGg9cj9RF9nGP/HKZaf8FKf24YXIg/aO8Q5zz5i2rj9Y6j6/Ax/1swkdT93bedMMJJgSTx83SpMxnhWzx2NfiX4Y/wCCsn7bGjGOO++KBvivVr3SbZwfqVAzXcaJ/wAFuf2rNDlVNU0rw1qC9WW40p4yfxikprGQN6PFmEqrVn69rKo4J6VLHgxADrivzE8Hf8F8dYiRF8cfA6xlP/LR9K1qSM+/yyoRn8a9j8C/8Fyf2T/E1ssfivTPEOgzY+YT6d9oQHGfvRNk/lVfWKc1uejQz/AT3kfbJJPehY4cbsAe+a8S+F//AAUJ/ZH+L6Rjwf8AHXQDNIQBaajeGzmBPbZOFJP0zXsmmazpuq2sd3YX8U0TqCrxSK6OPqMg/WtoNHp0cdhq/wAEi35fvR5fvSiSNhwf1pHIOMV0HUnF7CMpXrUZbJ4P5GnMQODUajAoGOUnI5puR+8NOT7wpQQEyf1oFBENSQd6bFHn5iO9TUGoA45FOF7ck4K02igCxURyTw1QhiOhpKDMlPp/WgeuabF/Wpxs/wD10ARMMMRSUrHJzSUGgUUo3e9AB9DQAlFFKCR0NACUUUUAFFFFAEIh8v8Ai61KpEXGc0tFACCQDtTfP+n5U4EFMj0pIYvegCT+H5loLKPuijeR94U2gB3l+9BXapptOX5vvUAAbaopCxPWn9un4VGRg4oAXc2MZqInPJqSigBinHJPbqaTzhz/AIU2DBeQinQg9aAI6ltiPvZp9R24HTNAFmAjB6/nSU2GXaWBPfihZOeOaDOA0HMRpE+6KQiboelJtYdqDQVOpP604Y70RjEXHrToxgUAJDwuMd6fRgZzRQAUUUUANZO4FIDg5pXb+HFNoASI9z60vWiigAqEznpnj6VNTJgSBj1oAjgzTl/1tNRT52PapIB3x34oAfUcfERJ9akqOgzK9OtDg8+tNyc5p0ZIce9BoWqMjOM0yEkuw568U+JiM7qDMbEw3uM00TDgAUgbIMY4yaZUpATK2QcmoaliHyfjTdqjtVDW5BUlmR+8GefrUkqElwoqv9kJOfK/SgsltOfMNT0DOOTRQAUUoDdQKVU7kUANop21/wC9+tG1/wC9+tADaKdtYdDTSCOooAKKKKACiiigApylV/ipF6j60gJByKAJMjOM0xjk0vme1NoARSMnBpajqReg+lABEwAziikUkjmnKpagBKKcVYfdNC7h/DQA6imt8q4FCdfwoAFAA3Ghfl+9R+7ptAlsPfp+NMp2V24zTaBiRxkE5NAUL0padGoA4oAbRRR1oAQcEnpzSJ3qRYhNnFRmIA9aCIDqKKKCwoopvkruzk0AMBMQ5H4URkpyRUtN3g/eFADT9z8TT4f9WPxpP+WdFtxI/wBaCOpDRSqMtU9BZXMZ7j9abF96rVVVidugoAu7lxnNQxSRFpBgcVAoIbpToge2fegCwBjgUUUUk7gFIXGMg0tRTHENDdgGtcE8fyqHzQTgN+tMYOegqKK2dTnpn3ougJftC5znp1NRTanbWsTzzXCqo5JY1hfErxjb/D/wRqvjXUgfs2l6ddXU+GwSsce7j8q/FT9pH/gqh+0l8fry60mw8WXGgeH5XIh0zR5zE7xZwvmSj5myM5HvXFWrOmfO5rnUMuj7x+rHx2/4KDfs7fACGRPGXxIha7i4/s3TmWe4J9Ni5AHHc18j/Ff/AIL26nNJJY/Bz4PmJF3IuoeIr8ljz97yYvb1NfnCmpXupu811NI0vO6R3JZ/cknJp9vC78kc+vrXBPMZrQ/PsbxdiJ6U2e8/GH/gon+1Z8bpJ4vEvxXv7PTpQf8AiX6TILSFc4GzEeXbjuTivGG1C+1CWW7u5y8jEsWkOXY+pJYnP41FFAQgC1MsOFyBwK4amLqz1Pn6+a4uu7zkUpI2kGX5J9T0psSHOB+lW/KB4A616D+zP+zP4w/aR+KulfDbwy5Q3V00lzcsCVt4RgNIf9lR096xjKdVkYalXxk+WO552IJANxU1DNHlzg8kV+wetf8ABHj9nXWvhhD4IsdFmsb6ONCfEEMpN68gC5Y5O0qTnjFfmj+1Z+yb8Sv2UfiXL4F8ZWitA0DS6dqqkmK9QtncBj7+MAjoD0rqq4SrCHMehi+H8bhaPtJbHkZgI6UJEynIFTBG6MO3NOVDkEA1wNnzfM7iIrAcAc+hoeRR8pI9ua6T4YfDjxZ8WPFNj4K8B6TJqOoahOIreCPnc5xnJ5xGOfm7Ac19n2n/AAQx+J03w9k1bUPifZw+IDbiSKyiss26vgfuiTySTxurenRrzV0exgsnxWLi5Q2PghWjkOwOCcdM06CPj5fwxXQ/EX4ReK/hF42vfA3jLS2tNS0+ZoriIknZIp4YHurAcVnW1hkcjiolGpT6mVWniMHUcJsrhHVVwxBGMHrivRvhP+11+0T8CJUf4Z/FHUbGOIAfZRe7oSPQxyZU/QVxAsscfhUcloGUgGtaWLq0i6OZ4rDyvBn258H/APgu98X/AA5PFZ/GT4Z6Z4htf+Wt5pc7WN0nuR88Tn6Yr7R/Zr/4Ka/swftHGPSPDfittI1eUfPo2tgQzn12tu2P+Br8QprXYpwuOtUYrqawvFms7hoWibcrocbWBHI57V2U8wq30PpsBxXiIW5z+lO1vYZ41aFwQQCMGrAIPIr8Xf8Agn3/AMFLvjj8MPifofw+8beMNR8Q+Gr2+gsnsdSuRNJbeaQqPHIfmJ3H7pyMV+zWlXYvLZZhxuXj8q9XD13Wjc/SMozCGY0eeJYgkIbBpHBI4pqHnjvTonG6TJ6dK7D0oXHxf6nkd6dTY5ABj1pwIPQ0GgUUUUAAAHQUmVAJBpMeZF8y96hrKmAwzspxv7+tWILhmGAciqbEk8063Y23Ge9agXc55zSBADnJotvvMB60tBmFKGI6UlFAC5G7OKSlII6ikoNAooooAKKKKACk2D1NLRQAUUUUAFGSOhoooAKUHBzSU5VYH0oAdTCpHWn01n7A0CWw2ijBzjFJ/wAsnoGBA5Oe1EJzD170xv8AVNx2psHBBPpQBNTBjyxj1p/A4zSR/dNAC0ltwSVoTkU22OATQZk/fp+NFFGT6GgtbBSBQOlLSZGM5oGLRgZziikgPUj0oAWiigdOmKACo+M1JRQA1U7kUmDjNLu2/LijzPagWo2iiigYU2GLDbielOooAPpUdFFBmV6WPluKSpbZflwR3oNCa04II9aapO6iIDycUL94UGZFRUsWBIwxUfRvxoNCeo6kqOgzCnxrx8oplWAAOBQA0KQQabUlM2sO1BpAVMU4AAYFRjr1xUlABRRQSB1NABgZzim/c980eZ7UmT6mgAJJ60lAJByKCSetABRSgE9BSUAFFFFABRRRQAu04zijB9DSx+TmnDHagV0R05Ov4U2lXORQMfRRRQRZjf4tvah+v4UE4JptBY5n7A00kk5NBxngUUAR1JDgjBqOpIO9AAQQcUU5gxP3aTBB9KAEGc8ULIB0NIsnPSiMkDigCxFJmX6CoKKKACiiigAooyPUVDFMxb5vzoAlZttNhBAINL97nb+tMDKeiNSSsBLUZOeTRnvmimA6GDfyDTqZ5Q7OfzpY+mKAEEQx8zH86ZEfKGCDipqKV0BXp9v/AEp7Fh90UFgF5PamKyHUVW845pbYZZ8c80romzsWCcDNVnfJ80E/nStMkULlm4yRn+leefFT9o74cfCSEw+INTL3QHy2FqweU/Udh9aPZuoc2IxuGwy/eM9BG5z90flSwKJeSOM14j4M/bk+E3iW8Wy1D7fpJbhZLpAV/EjNex6B4g0LxBZpfaLqsdzC4+V45AQfypuhynPQzPC4h+5Mo/EPwHpnxI8Eal4J1ZnNnq+mzWtzsbDeVINjYPrjJFfjv+19/wAEf/jx8AL658VfDvTJPF3hlRmKbTo83lmmeFlh53kDq65+lftRD5YP7roeMClurOG5hMLoCCMcjpWE6UZ6M581yrDZpT95H81s+k3mmXElpdQsjRsVmRgcqwOCDnkEelOilQAKB9K/b79rD/gmn+z3+05ZT6jqHhoaRrxXEOvaPGsc2T/z0X7swPvzX5o/tP8A/BKn9qn9nhZvEGkeGE8WaFF8zX+ikl4lyOZrcjdwM5KnvXjYjASWqPzTNeFauGXNRR882rlldi59ualjcMOtZ0Zu7QyWl3C0ciMQ6OpG0jqOemD61LFdbVAJPSvLqU3DQ+VqYerR0kXIQGO3jOa/Qr/ghLo+jXnizxjrFxErXtpptpHC7Y3Kkkj7yPYlBX53Q3kZfrnntX1d/wAEjvj9Z/CP9pa00rWdREWn+JYH0u4Z3AVZHO+Bjk8fvEdPbeK6cBZ1NT6DhqpCnjIqXc/aCKMCIKAK+Tv+CtX7Pll8Xf2aNR8VWdmDqnhfN9bSKuXMQA8xM+45r6tsLpZ4VdWGSM9entXCftPX2l6f8C/GFzqxQW6+G70zbzxjyGH88V9FUjGdHlP1fMqVKrl0r7WP575ERG2p0/8ArUWUP2hyFORnBxTjH5sEYAwWQHj61u/DXw1/wkPi+y0CMHN7LFCvpudlTP6/zr5bkvUsfhtPDqrjvZrufpf/AMEc/wBkaDwd4FPx/wDE2mKdS1seXpKNHzDa7uWGefnOTX3xLZRrFtRQecAVznwk8J2XgzwVpHhbTLcRw6fZRQRKowAEQD+ea6pm4ww/KvocLTUaZ+4ZNldGhgFFLU/Mn/gtT+ztDo+t6P8AHrQ7XbHdxnTdW2r/AMtB88L4Hc/Mtfn1bYDFVPPpX7M/8FWfD1lr37G/jHz0DPp0dvdxMByrpKmD+IY/lX4ymVY3YjGMkA56V5uPgoyPzfizDKji7ok2AdMimlAT9O9AuV8sEkHjrUMl4V6Y/wAa8uSbPio3uVrxQAyisK7gEkxbHRwMgE4Pbp/k1smSe+ultLZC7O4VdqbjkngYBzkngDuTX6Sf8E5v+CT8vhm90346/tDaLBJe7Fn0rw7cLv8AsTHaySynOJJOvy4wvSurB4etV1R9LkuUyx0tDzz/AIJYf8Ey/HWreMNC/aK+Mumyabpum3a3mk6BdoRNeHaPLll54QbtyrjORk1+rttCtrDsi6AcVV0vSotKt47W1gARIwoA+mMVYubqO1iMzkYxnPrXt+2o4GheR+uZPlqwdH2cNxqXUiplwPc01dRhUnDDI65I4r5b/av/AGx7rw3HcfDz4Za3m8jYx3+qphzAc/6qP1f/AGu1fNHhz47fG3wfrq6/pPjfVFm3B5DdXvnLJ04dDwc+1fk2deLeU5Xj/YXT+Z93gOGcZi8Pz7H6frqHy7iv0qWGTcgAPJr5n/Z3/bn0Dx3ew+GPiNAmk6qRtjuAx+zXJ+p/1bHHQ8V9Jabe211EJbdw4I6g5xX2XDfGWVcQQvTnZnlYzLMXganLURbQ8AmnggngVHvU9COfSlEgB5avuFrE4R65xzTPKG3dinb164pI14J9ayg7AQpED5menbNER8r8Km2N6UwxKT7/AFrYCGznUNu83HtmpbU5Y4bPOc037NzkEUkAKuOD19KALVAJByKRZOelKAScCgzHeZ7UZ9v/AB6mkEHBpcn1NACUUUUGgAE8CipYOh+tRUAFFFFABRRRQAqjJxS/99UittNLuXbigWtw2kH5aAxHDUeZ7U2gY8MD0NI238abRQAUUUUAFR1JRQA0xKX30sX9acDg5NJBjnNAAQR1pqMAPvU5ziJgaNsXoaACgEg5FLuOcikhHUEUAFAJHQ07Zntj8abQA5X/AL1KNq8ZplOUdiv40AOooprYXotADsn0NIXA6Unme1NoAUknrSAkHIoooAMHriilictwaSgAooooATYPU1Gpz+dS02QcDC96AE8rHGBSUE9yaKDMZHncFz3qVODjNQQ8tT4UMZx70GhKSAMmoQOcj1pc8df/AB6ktgRHt9TQBKVY9TTaeuMcUygBVxn8anBB5FQgKOd1Sp90UGYtI2McihTkZof7poKiMpyso4pvSg9euaCh+8ehprHJzSUUCsgopdrYzijB9DQMSlBI6UlAOORQAuTjFJRRQAUUuT6mowMnBoAQgjg1JEeOfWntjHNN6Hg0AICR0NAODmgAk4FO2v8A3v1oAbRS7SBkihRk4oASjnNSAADAooAbkr945pMn1NPwMYxTH+8aAEooooAjqWLpgioqkhyHagCSim7tvy4o3bvlxQAzygPWhOn404KW6mkIIODQAUUUUARRHgEU6VsU5hkYquYiD/qaAGVLByP8aXnyu+cUkCfNyaV0BOMfYcj+fvUEMoAyePrU2MD5RUIQ8mmRZi2/XPqacCfKJHoaWLAAA9KfS0SLEXp0pakHPTvUdD2IhcKCQOtGR6imswIpJFiswUVVnm4zmpyfkyf7tVpACDmh6qxO42J953NyPrVXUNTtNFs3vLydIlRS0k27aAPUnsOKzPFvjbRvBGjS6t4h1KK3ggQmSV/kH0r4y/aJ/an8RfFnVJNC8OTT2uhwvgQxtiW45wHfvspUqdndnz+a5zSw1N23PS/j7+2o8NxceEfhfdcsrJNrRO8bumI1/wDZ6+adQ1C+1S5m1DUb97m5lbdLNK+53z7/ANOlV4ImJAzx7dKspHnnnjpXXdrY/McwzrEYyTIIdycrn8K7D4afGjx98NLsXHh7V3RAfngkJaJx7jt+Fcv9nVvujFGwxxng/hSd2cdDHYjDvmTPsj4Qfti+GfGVvDpviwf2XeOVU73/AHbk+jjpn0r3DTdXtL6FWtZldccENnj696/Mi3mmijxA20ZyT/WvQPhj+038SfhqgisdYF3aq3/IOvssAPVX6g81HKmfaZVxRzRUap+gg2NbtjkZqDUNOgvYWguI1YMMcivGfgx+2N4E+I0Uem67MNKvmIVoJ5PkYnsGr2qz1C2uYw0MgYEZBHpWcoM+zo4vCY2mkmfJf7XX/BKb4NftGm68SaFpq+GvEboxj1fT4gUmcjjzouFcZ78EV+VX7UX7IPxv/ZT8StonxK8FSR2RfFpr1k7y2d36Mp6xk4+63TNf0HSyR+XnjFcp8QPhz4T+JGhT+H/Fvhu01Oxu1KzW17EpRl6chvbuK8+vhIVEeVmXD2ExUPd3P5xzfFEBHp19ak0vXr/S9RTUNM1FreWJw8citjYQQd3qDwCD2IzX6cftff8ABETwr4lsJ/GH7Mco0fUlZnm0W+uN9pOMfchPWM5PBORX5w/E34H/ABO+DXiubwr8SfB93pWoW7OFguEOGAOdyOOJAfUV5k8PLDH59i8lxmXV+aJ+pn/BOn/gqPoXxT8PWPwy+MuuQ6d4lsYFiF7Ov7nUEXAEm/OVlPQqeKzf+CtX7cmgad8PZvgH4B1lLjUddiC6tPFLuFvbd1yuQSx4yDX5ZaHeX1jOJLad0dTkMrFcEdMelX77W9T1e6a41TUprlsY8yeQs3555qXjKns7G9fiWusG8PMWORWYKUwAAAM9AK634H65Z6P8WPDuoXq4ig1yzklb/ZFwmf5/pXFCTC5L5z3p1rez214skMxSRWBVw2NvPB/A4rioyTqnzeXVLY3nZ/R14Ou4b7S7eaBwwaMNke4/+vWtIAB0+leE/sDfGrT/AI3/ALOXhHxpbXIaaTTVt9Ti35Md1EAkit6Elc4r3O5uYoYSzn5QK+noNexP3jLsRTeDjO58r/8ABWbxJYeHv2KvGaXDqHvvs1nEM8szSqcfkua/FyW4Z5CQ+Tmvvr/gsn+0/Z+PNatfgB4auxNbaNfG71iaN8q9zj93CCOu1eT71+f9wAp3g8Z+8O/evFx9RTqWR+V8W4unXxvLEma4kJ2Kcn0Heola9uWjitIzK7sE2BCSzkgLwOeo6Dmrnhfw7r3jXXLTwt4c0ye61C/uY4LWC2QtJLI3Cqo9+56AV+pv/BPj/glXoHwday+K/wAbtNg1PxLGge0058SQaaThh7SuMkbux6Vz4bB1a8tNjysoyLEY2qrbHnn/AAS8/wCCWmqaJ4h079or4+6UyTW8i3Hh3w5crua3Y4KXE/PzEAnan8PXrX6YRWkcUAiQDAHAqHT7OG1tUhiXChRgVK11HGGDOOOpxX0EpUsHQs9j9eyrKaWCpqEFqMvbqKxt2mlYAKK+Wf2r/wBrJ9Fe68BfD3URJeSFo768R8i2B4KLjqcd+1Wv2tv2p20h7j4ceBL/AH36Hy768jORbeqKe7EHn0r5Qa3mmunuriZt0mS25s5JNfzZ4n+J9PCRlg8LL3ttD9V4Z4blWftai0KMemyPLJczXLuzfMQ7Z+fux56+9KtjiLpyB+NaAgwdoag2xIwBmv5Fx+LxWOxLq1Zas/VqGGpUKSjBGV9mZW3R8H1PSvZvgJ+2f4v+FcS+H/GKz6lpMPEStLme2XH8LdJBz908ivKpbTC5XgVTks0IcN0yTgdq+i4Z4wzHh7EKVOV0cOY5Th8fStKOp+kHwi+NfhD4teHY9d8I6ss8LtiUN8skbd0ZCeD16V2qTK6hkPB96/Lr4Y/FLxv8FvEa+J/B+pnLn/StPlkPl3K55BPZjnrX3n+zd+014O+OGjlbWQ22oQLi906dsPA/rzyQfUV/ZPh94mYPPaEaNaXvep+RZ7w7iMBV5oL3T1kSMBipIQC7jPSq+0HO055p9uSPMI44r9qpTpVY3R81rsyc8c01vQt+GKMgr8xpoJByK0sgAdeuKegwPrSIe1OpNsBifeFPBIORTBwRkd6n8sheTVGYznHtSUEk9TRQAKwwQKaeJsClXv8AWl4oCA+E5yvrTKKKDQKRiQOKXJxjNNbPlfhQA2H/AJaVJUUX3VqWgAooooAKASDkUYI6ik833NAD9rDoaF/3KFw3VaPu87P1oAGyvRqbg4ziilU4NACgcdDQ3y/doOV4VaN38O2gBAcHJpCCOtHSnN833aAG0At3x+VLtON1JQA6PvTk/wBUPrUdOtz85O78KAFIBOaRU7kU6igBvl+9Cdfwp1FABQcd6MjOM00su7OKAEIA6HNIAScU5v8AfpoBJ4FABUZ5zzUnToacFAHzUAMEgBzijePQ0bB6mloATePQ0nme1NqSgAoJxyaKCcDNBmRowM9LCctIc/jUSn9yRUlvgB+e1AEI/iqa36fhVcHPIp8KjOT3paM0GxNiM896ePvD603YRyGp6jJH1pgTg5GRUdSVHgZzigCMEdjVpGOcZqt5cY6H9amt4geOvqaAHb29aVfm+9TaASDkUAObb+NNpyt6tTaACiijrQA7PldfWpbc5G71qE5HGaQE9jQZiv8AeNJSv940lBoFFFFADMn1NOh+9imUqDngUASbiOnFL5fvSBSegpUBBoAFVgfSnDp0xRQenTNAmrjWT+6KVV2nNLQBgYoFEKKKBjtQUFBIAyaKaz9gaBXQ2iiigY9RhaZnHOacqdyKYR5ZB20ANizkY9KkB+bJpEICYHeigB3yqvrmm0UUAFFFFABSbQevNLRQBDHnHNCcAmnH7z9uKqvn0rH7QCOTknP61JZnzSW205FysnPalt0MWMDFbATRfcp1FFABTfNj/vfpSscCoeRzigB2FA6U48kkCmByTg05SSoyaTdgIiirisXx54v03wN4YuvEGsS7ILaOV5W77R0rbkLK2QM157+0p4bv/Fnwi1vSdEiaS6bT28hQTy3BOPqKVKz3PPxlaVPDScD4y+PH7Q2u/F/XJSXkttOhYmzsSflZR0Zv7xPvXA6YmTuyfXk1BeW11a3fkTqQQ+GRxzG3Qqferulpyw9DgV1Rgj8bzHF4ipiGpl6GBXUtjpUixgnBNN08sYn3HoaljBLYFDRwJRaGR/MBmho8sw68dKkjiEakGUfiKdpOmajq94lrYQSzTTSbIo0XlvSpciqNCeI9yO5SjDqzcn0GKrSEhzg8+ua+jvAf7DOu6toT3/jDVza3U8YNvFbDb5ROP9Zz81eMfFD4X+Ifhd4luPC+u2gVo+Y5wvEycYZf896adzuq5LisJQ9pI5GJ7lJG8mQrk9Qa9a+Cn7WXxJ+GKxaZd3Z1fS4xj7HdyfvYx6o/f6V5ZCjKny/malih+ble/emc+EzTF4Sd4M/QH4R/tF+CvixZxvo18ILnH7yzujhlPp716NEiTKGPPHGa/NDw3rWreHrkaho2pPBNG2UaN8MD/WvoD4P/ALcesaTDHpPxJthcQqMC/gHzoP8AaXvWcqaex+gZPxNSqLlruzPrAwIVMW0EdMV5H+0v+yT8Kf2lPCVx4c8ceHI5pCD5F2qhJYHxgOj4z+HSu78DfEvwn4901NW8Na3FdROMko/I9iOoroxIHUAnjHeuapS5lZo+o5MLmEOlj8PP2wP+Cb3xk/ZdvbrXdM0ebXvDQYmPVLWI+ZbjsJkAOT/tDivmlbhxnJyTk5HQ+4r+kXXPDWkeI7CbTtV0+KeKQFJI5YwwcdMEHqMdq/O79t//AIIsW/izUL74kfszCHTb590t14cnwLe6c8loW/5ZMegU/LXlYnApRvE+FzzhhtOVA/MpZty7twI9afHN5YyHIz364rS+Ifwq+Ivwn1648MfEHwnqWl39pKVntb6HYYwPwG8cfeGRWEZ1ZcqwPuO9eM4ulLY+Aq4evgavvI+qf+Cbf7e+pfsr+Mbjwl4rmebwrrL77kmYj+z7gAr54HOd3ce9e5ftXf8ABaTUvEFvP8Pf2ddPltbaSIxXHia9OZGHQ+TH2yD98+vtX5yxja2VOM8jBqWNjuyx5Pv1rWOPqKPKexR4kxVKh7KB2Wr+Kr/xRePqOp3Mk7yM7NLNIWaWRvvMTnn1zWa+lX+pqbbToC8hKgFULGQcfKoH8TdvoaTS7GbUWS2to2YuQqqi5LEnAAHfmv0p/wCCZ/8AwTnPhOSH43/HbwwyarG4bQ9IvFVltI8gid8cF2z90/dHvV0aE8RUuGV4KvnGKcpI0P8Agk7/AME7b74R2kP7QPxd0bb4ivYsaPp0yfNpts5yWOT/AKxwee6gV9/x20caBYl4AwAOw9KrWMSQQJHEoChRtHoMVYeeOOPcx4A6+le+p0sHR12P1zKsup4KiqcUQXVwtrExd8Y/WvmX9rD9rweFLq4+HXgG8Damyst7eoQwtc8bR6sQfwrR/bA/aog+Hto/gHwXfpJrc6ETzBgws06HP+17ds18Yhru8vZ7+7naV5WLyPK+WZyeWJJr+cfFLxMjg4SweDn73U/T+G+H3WarVVoakVzNfSyXV3Lvkkcs7SEs0jE8sT61IUDDBB6d6qWbkqNhJJ6Y71aWVnbY4w2MkGv5PxazDM6ksVO7P0zDrD4VKmhpQiQADtTirDtU0agtwe1GFxnFeNJO+p6lN3WhXdTjpVaaPJIxirzqcYqvJEMtnjis2kW2ZM9uGyCM9sGn+C/GniP4Y+JrfxN4Z1lobq2bMbKOq8ZV+fmB/HFSXKsM8VkXIPzEkn+tetkeaY/LcZGphpNNM48dhaGJw750fox+y1+0Po/x28INqABh1K0cRahZM2djHow+vNeqhCwyTnnrmvjf/gmd4Z1eLVda8VbHWxezEDFiQHlV+D9cHrX2UkqbM4P5V/oZ4dZji80yKnWxHVI/B87oUMPjZQgx9JuX1o3AruHpxUQUiR8dgP51+inkkqyDPFSB171BanIk57UsQ2ng/rS0YE24Y3VWjJNz14zUwIK0kXTgUwJsL/e/SkAycVHUqHcufagzHHIjfFRRjA6076UUGkAooooAKKKKAGNKg5BFRWsuT1zmpDbgj71SUAFFA54ooAASDkUAkHIopRnqO1ACW/IP1pX+8abCQOR60pOTk0ExCgdeuKKBjPJoKHAE/wD7NEfenDp0xTWf+6aACTtR9/2xTacp6saAEMwBxtpPNUnofzpmTnNKpUclqAHZPXNJuU96Wo6BWROh46UtRwd6en3RQMWjAHQUUidPxoAQttY0mTnNDdT9aTBxnFAB5oY/doopIv60APj706kAA6UtADXX+LNIwwcU+mP940CWwlJsHqaWigYUyJg0shX1HOaec4yBUVvE3ldTnHegzFbuQPyqBhg8VMk5j4xTQMx9OfpQaQI7YkNJinowzkfjTrdBuZcDk0WR2MwU0AMi5QmpQMnpUaxEdTUlAE6yHOQtNz82VFSDb3qMn5sigzK5AMe72qbT3YjGaUDPApiRY5zQaEm1uuKSnkLjpSKrA+lADaKdt+b2pGGDjNACUkPXFLSQg5zQAsRy5NSRY2Go1yBx3ooMxTgcqaSlyfU0lBoFFFFABSW52tnFNT7wp8GQjUASUEAjBopAQehoAUADgUUU1iQ3DUAG5R0FAP8AdX86FfsTR5ntQJbDqKarKB6U6gYxjk5zQDg5pQnqaGTuBQA2nfvKTA9P1pY+9ABu2/Lij/Z3/pQy/wAQH1pw6dMUAMI2nGaMn1NPphGDjNACUUUUAFFFFABRRRQAT8KBVE5/8e4q3NyvFREEcGgAtgDjH41YqKyGFkPtUoIPIoAKKKKAEIB60ypKa5AXOPxpaJARowIdFAJHQU2KVFVw7jgcUz7RHBbvPKeOTkV8hftb/wDBRif4N+LpfBHw70m31i/tDi+uLuQ+RbscYiCpzIx4+lcOMzHD4KN5nHWxNOh70j6/TcxBIOPcVXu7YXMTpjqOK+O/2bv+Comg/EHxLa+Efijo8ejz3kgjtdRtp2e1dicKrKeY2Pb8K+x7K6ivIfNjPBHGT7Vjgsyw+MV6YU61HGU/d2PlP9r39luOe2f4n+A7IpLEv/Eys4l/1i/89Bx971r5t0x1UujcEHpX6fXenx6hbNb3FuGDoVIbp/nFfGH7W37MP/CAaofiH4St2XSrl/8ASrVB/wAe7nuMfwk17VGp0Z8PxJkit7Wmjx6yKrA5B6mlhm+bkfjVWMiIeWPpT4ZwFfB7Vs1c+AknT0ZejVZB8nNfR/7E/wAJbO9ln+IesWiuYJRbaeHXOW6s364r5psbpVYFT0PINfd/7J9vZ2vwV8PTRrxIkkr8dWZiM1hJH1vCeDpVq7lI9LW1WJNgA46V4f8Atn/C1fFXgYeJ7G1H2vTFyz4yWhPUV7s7gnb/ADrI8VWMGq6DdWEyhleN4yD3yKzjP95Y+9zPB0quClE/M6WIxM0fp0J+lOhZvK25q94lsfsuv3duD8sV9dRqPZGwKz4yQSq+tdbaPxarD2daUexPHIVUY6460jSsXLHqOh9KaMY46U0hj3J96xd+pNOM09Da8D/EbxZ8OdX/ALZ8K6vLaTI37yJs7JfqOhr6w+Af7Xej/EUReHvFCJp+q4wAXHlze4J6E+lfGyQHIyTT7eS8spzcWkxjKchlOCD6j396tQbR7WVZ/iMHV5ZaxP08sruO4RXjfIxUzRRyZQhSSO9fGvwC/bK1jwlFDoHxGuWutPjKpHe5zNAvQbv746819aeEvGWgeLdLi1fQtRiuYZlykkb5Fc86TWp+nYDM8NjaaSe55p+09+x/8Iv2pvBdx4U+I/heOWXy2W01GHCXVo+MBo5Bz7471+O37Y3/AAT/APir+yB4ldNasX1Hw5IxGm6/bwkRyDPyrIB9x/c8Gv3pLqxIPOOOTXN/EL4f+FviJ4du/DXizQbW/sbmMpcWt1EGSQEYzz3x0rgr4WFSPmcOd5BQxtHmjufzfuGhlMUvB6hT6dqcsqbfvdc4wa+8P27v+CO3jLwGtz8RP2ZNOl1XSkJlufDgYNdWq8EmEn/Wjr8pPHavJP2Dv+CcHxS/aL+IMGoePPD99pfhPTpQmp3N3ZvA8zgqHtkVwGJP8T4wvIGc5rxHgJupY/PHw5XjWUUj1/8A4JEfsa6r8WvFVr8avGenyW2jeHL3NkJU+XUJ8Yzg/wACg5yOpr9XLPSIrG1S0towqIoVVA4AxjFYPws+H3hz4XeErHwd4V0yK1srOBYYbeJQoUAAce3FdU0mAQGHTgmvapxp4SjZn6XkeV08Dh1FLXqVSwto8FsBR3r5/wD2s/2tIvhday+D/B80cuu3MfcgraIcjew7n0FdT+1J+0Fpnwh8NywwzRy6tcqVs7XcPl4++w9Opr4H1nVtX8T65c+ItZvHnubuRnuHdydxP8h6CvwLxR8R6eU0Xh8PL3mfqfDfD8sW/azWiK89/q2r6lNrOr6g9zPdMXnkncszue5Ofyp8WF5A5pYofl2ntW14E8D6r4/8U2PhbTfluL26S2jZf4RglnP4V/JuCWN4ozrlk7yk/wBT9NqOnl+BbWiR6F+y/wDAC++MPiJtU1SBotGsHBupB/y3cdIx7epr3/43fsj6D4k8JtJ4Y0yGy1SxjLWbRIAGx/yzb1znGa9Y+Evwv0T4Y+EbDwtpFuEjtlXc2OXfAyT65Oa6aeMSAxEdepr+wsh8L8BDhtwrR99rsflWM4iryx14PQ/MS4s7yw1C4sNRtXimt2aKSJuscgOCDTYyrDr2r2X9tPwDb+DviT/bmnwBYNai8yQAf8tk4JHuRzXi0bDBVTg96/kzjrIP7BzmVJLQ/U+H8d9cwSk9xajkG7IqSmOe5OB6iviuXn0R7bkitJGOp5BHU1qfCf4Q658YPGkPhHRIH3NIGuLvYdsEXRmP9Kn8D+Ctc+IPiS28JaBal7y/mwE/5ZomMbj6Ackmvu/4A/ATw98FfDCaZYQpJdzgNqN4R880nQgf7HpX7V4X+HeKzvGRr1Y/u/M+L4m4ghg6LpU37xqfCL4W6J8KPB1r4W0G2EcEEYWTI+aRu7H64Wuq3hVAJ4I602fCDg49hXkf7T/7U3g39nXwz/aesXLT6jN8thpkUmGmbsT6JwMmv7Yy/DYPh/L1QWkYn4rjMa6tV1Znrok5wM1GjiMue+cV8L+B/wDgrFrlx4hih8Y+AbRLF3/fy6dcuZIVyATh+HIHNfZ/w/8AHWj/ABB8P2fizw5drPZXlt5sTjup6E+/bFb4XOMJi5csZGeGxtLEaRN22kOOO9Twnc2arWoxGBmrVuSIfxr1qbOslp5YDg0yitjMi8rnHnH8qcpwwNPpi9R9aDQkOQeR36U+mP8AeNJGCIQaDMU/MeBSU8gMKrQqVwaDSDJqKKKACikTp+NLQAdKKKKACmQnBYfXrT6aFJbI9awV7jW42GNhyTUlFFbiCgdeuKAccigEg5FACq2ODSEknJpWAHT+dJQAUUU0SgHIB/KgBwgJ6MKb5RHU1KJs/wAIplACeYvpSg55qOpF6D6UAPhbAyp7+tLUY5PI70/cvrQApOOTTY+9G/PfH4UJwCaAD7/tinUCUngKKMDOaAAADpQMdqKKAAdOmKRjgUtNfNACFiRikoooAKKKKAIlb5JMHtUHH2XG7knpUxX9feoCBg0AOtOlWFGT0+tQ2uAH46DNPhuRjnFJbATYwMCobGMAls5+tP8AODfdplkSWytCVgHZGcUUUUwJKKKKAEAwnHpREcAHNH8H4UkMeRyTQBN1o4UUAYGKaWAHy0ADP2BpuTnOaKKAAEjpQCQcik2LTKAFJJOafUcIyhAqaMfIKBNXI4+9Op4ULTXK5yDQMSik3r60tAEdPiPp601PvVIn3hQZi+Z7Uitjg0qA4oKHtQaB5ntTevU05VYH0pwAAwKAI6Kcy4+YUKpDfSgAUMD92hd34U6igAobofpQOnTFFAEZBHWgEg5FOZfRaaCR0oEthy/7X60blHQU2gEg5FAx+8ehppJPWkOM8CigAooooAKKXB9DSUAFFFFABUT4281ORvOOgHeoetBCvcIQYVk57daWFsjBNJDhmcHnJohGwcdCaCySiiii9gIT+6aRsdTURn+XJ4471NKAQc+tZWva5aeH9LutS1S6SOO2hMsjk4EaYOCfyNYYquqdLmZjK1NHkH7bf7RafAf4VzyafOravqkptNHi7oxX55CPRa/LnW72/wBd1WXVtSuHmnd2cSuSS0jH5nP1FetftZfHbU/jt8VL7WUnDaVZzNa6TFuzsiU8t/wI9D6cV5fFp7y4B9M1+NcTZ66tZwiz4vNsdzy5EY1lbvZSJJBlWXBUgkcjoc+3rX6L/wDBO39rdfinoTfC3xlqW3XdIt18l5Tg3lr0DjuZBjDe2DXwKNHYDccfU1o+BvEGt/DXxxYeN/C961rfafiWKVW/jY/Nnn7pQEEe9cORZ3UwmITb06mWWY6WGnrsfs5bSKYlbAIYDHPWsvxf4XsPFmh3Gi6tbLJFcRFJA46g8fnXn37Lf7ROi/HvwBb67ZTLHewYTVLPeN0TgcnHoSDXq8mHhKcYxX7TluPpYympRZ9i1SxeGdtbn53/AB++CWvfBrxfcWRhaTT508zTJyODHu+ZT7jj8687guXCuu/8+9fpB8YfhRpHxT8JT6FqcQDkFre4IG6CToGFfn38Rvh/q3w28V3XhzWdPdZLaTYGAIVgekgPcEA8e9ezGd9D8r4iyerhKvtI/CzHtr7nlulfcf7EHjWw8S/CGx0pJgZtIuHtrlD/AAgncpP1r4TjwJCDzzivR/2Y/jdf/Bvxybu8md9Nu3EWpRZ4MZPEg5+8vr6UnFsw4ZzFYLFpTejP0T3q53qDz61g/EDxJZeFPB+oa5eyBUtbZ5pSTwDjgfiateG/E2leJdKh1XTLyOaCeMPHJG+QVx1rwT9uT4qx2Ohw/DXTJD9pvZRNqBD/AHIVPyqf944rNU1Fn6bjsfRjgpTufL2t3LXt5NcsPmkmllf6yEE/1rIBYdBn6CrrO7u24E7uv+Fdd8C/g1qXxh8ZpoiRvHaQbZL+5AwEizjaPXcPSm20j8np4WpmONah1LnwJ/Z68Z/GWfdZSra6dHNiXUJo89CMogH3z/tdBXq/xb/Yn03TPDC6l4BluDeWcRN1DO+/7QF649DX0f4I8DaN4D0Wz0TRbFIIbeMKFjXhAFxge1actruUqyDBOT6VLqdD9Cw3DGHjhbSXvH5ovEbG9ktpICGXcrpJ96NxgEVG2TEfevZv2x/hZa+BfHK6/plqUtNZZ55MdIpkOGUf7wO78K8WjlzE4JyQTzmumDXs7n5/mWCeCxEqbRTnhYt8rEHsfQ113wg+PXj34P6qLnw/eGeyaTFxYzMfLlPcrno3Ncu3POc1EyA8HnIqHqcuExmIwk+aDPvv4GftIeEvjBpwaylNveIP39jK2HjOP1r0cMZF3MTzzX5n+EPFereD9Sh1bQ757aeA/JIjdPr6ivsv9mH9pG1+Kmnf2Dru2LVbeIMyg8TJkLvH1Nc84qx+k5Hnyxn7upuevG3SUESoCM96r2Omw2YdII1AYksAMZ/KrYIcbgeD2xQikM2TgetZJU2fVQw9JvmIkYr9zj0xXnP7QP7QugfBTwzLqF/IJrx18uztFbmWUg44/u56mvRZi0cRYjoOOa/OP9pjxb4x8a/GrUpvFVnPbJZXMkFnayZyke/hx7NX5V4kcSYjIsqlKj8TTPpOHsup4zE8stjF8Z+OfEnxK8SXHijxRqEks1zKXZWckKO0ajPCisyOEBiAMYHWnQRdOKfEFJIZsc1/A+e5vjs5xjq15XZ+34HB0MHhuSmhkcagke9ewfsOQWt58fdP+0DcYLa4dMj+LGM14+CS2EfGe9dn+zf8RrP4bfFnSfE2pKUto7s292+escg27/wODX0vhtiaOH4lpSqbXX5nm59RnUyuajvY/SRRmNUGOgwR6Uwp/Dt71HpV/BeQRNDIrh0BUqeMdvzFWZ9ijcenc1/o1gcVQqZZzx2sfgtWEo1rM+XP+Cidtbx+HNBu9gDpqkiA45IKZP8AKvlC3lLE4NfQ3/BQfxvb614n03wbazBm02KS7ucHkO5Cop/4Dk185258tDk9e4+lfwn4y4vD4niCXsuh+zcHwqQy9c3UuhgRk02zstT13U4ND0q2ee7uJhFbxRLy7HoPeq5uSwKIeccFQa+tv2Ov2Zf+Eatrf4m+M7LGqXCZsYJP+XeNsEMf9oj8RXz/AIe8FYziLM4ycfcPRz3OaGX4Rr7R2H7Kv7NFn8KNHXxBryLLrl2g8+Qf8sEPPlqf517VIgC7W+72+lNtVMShQMjHfvVLX9e0zQdIutW1O9SK2gR3lkkOFjRRyT7cV/efD2SYPhrLFTiku5+H5hjZ4mo6s2cd8f8A4w+Hfgp8Pr3xh4hmAEMZFvHnBlkwcKB6ZxX5S/F/4reLPjf8Qb/xt4x1B3nmc/ZIM5SCEn5Y19PevWv21P2nZP2gvG0tt4fvGGg6TI0WnR7v+PiQHmYj09K8MisgiZOfxr4virP3Vm6dN6HwuZY5zbjErW8K25DKMHOa+sv+CcH7VTeE/EQ+CXjC626ffuW0a5dv9Xcn78J56OOV9CPevlcwIVOR+NNtbm60i6i1KwuXikt2EiTRsQUcEEMMdx7V8pk+Y4jDYnmuebgMZVoVkftJZ3UE0G+Fsrjg/wBKt27gR4zXgv7D/wC0Inxu+GMVxqzhdV0iVLbV4h1LbfklA64cc/UGvd7YIcCU4x15r9yyzGvGYaNQ/QcNNVaXMi3UFqBucCp+MZU5HY0V7JtAKKKKACqVt8jD5u9XarKQDk/3qALQBI3CkIIODTomAzzQW/8A1YoMxtPtT8rkUyigAoo+lFBoFFFFABRRRQBHDOE+U1ICDyKZ5R3ZyKLaIDtxigB9AJHQ0ifd696WgAooJJ60EknJoAKKKKACil2sO1G1vSgBKj8zB5NSjr1xS/Z1znK0ARxkSjBp0XK7felWIr0NOUEDBpJWAYOvXFOVMjJNOopgN27fmzR5ijsaME9/zWkKbRQAq4K/dpwAAwKQADpS9KACkY4GaWms/YGgBtJE3m+1KcZ4ooAM+UOaKKKAA4xzTXI+6BS7FqM2/wDEVNcmpHKyvkA8mpbVxtkDGoW++KWL+L6V009iyS1+4frU1jNkcio7SMeSeenvUlkqmin1AYoIbFOprHacinQd6oCSiiigBP4Pwp0P+qHXrTeGj/CliOByaBPYdJ2puTnOacU/umj5vv0AtiNRuOSKcCR0NIitjp3prLjkUDJFw6kj9aYIyTgGkAJ6Cnx/L96gBTwNpFC9R9afTV+b71ACghhUTqfvCnxZ5z608jIxQBXpQWz1pdnvToYwp60AEYHSnJ1/CmITu/Onp1/CgT2HUUUUDCgADpRRQAYHoKau38adTW2/jQAoYHoaT7nvml3j0NLQA1U7kU4dOmKAMDFIAQOTQAtNk7UeZ7U2gn7Qq9R9aQnJzRRQUL26/hSUZOMZooAKLT734UUQ/wCu/GgB3Lr7004zxTsY4B/A00gg4NBmFOJ/dZB7U2oZCw6UAVmTAJBpI2Kgj3pSxPelhiBBPvWcDQmtnJBBqSEInPm/maYARGPpUUUXNaAWPO9qYk/G1qPuDOfzo359xSduoEZnRMl2x6V8e/8ABS79pdvC2jJ8E/Ct9s1LVVV9TlRvmit+QE6/xc/nX1H8QfGGkeCPCN/4v1udYraytZJ53ZsYRQcfmRx9a/JP4sePL/4t/E/VvHerTEzX9000QJzsXPyKPbbj86+J4qzX6thXCDPCzTF+yg0Y9nAH+4MZX7ua0bOzGGyB+NN0+0wvJ5A6VbjXyw+RX4lXm68nKR8PzupUuxvkgdR+lUbpAIy2e5P9K0XdSuRVKUtnjH41jBuD0K+FnR/s8ftCeK/2ffiRB4m0O5Z7ZmVNW04nK3Nvz5jcnhwMBT9a/V/4a+OtC+JngrTvGPhy/jnstQtlmidCDlSPuk+oOc/SvxmvrQCRmA+YtkkZ4NfR3/BPD9ry8+FPi2L4V+NNSb/hH9Xm2W0k0nFjdk4BGf4ZOmOx+tfpfCedxpPkm9D6vKcdGEeRn6WFUKAEDpxmvDv2sv2frL4keG5dZ02AnUrGNjb4A+dMcp7k8817LYaml3b+cOB9addRCdSCQSR1NfrVCvGrDniermGDpY/CuMkflfeW02mXUlpNAUeNirqwOQQeRUcMhRso3r1/WvpT9s/9nWLSZZvif4Vsz5LSFdStlHEbnpIPr3r5uSLDHPUda9CM+aNz8bzLAzwGL0PQ/hT+0X8Svhjpz6RoGvGS1/5Y2843CLPoT161jeIfHGveMtauNb8Sak1zc3Th5JucAdoxz0FczABH9zpVy3cMoIP61LdzKpj8VWp+zctDW06EXEqx+tfaH7IHgCDwr8OYtYa323Opv58hI525wo+nFfHHhCBLnU0jx9/YoH1GK/QzwFpqaV4esdPVABHbRovttVf8TWdTQ+v4PwqqTlUfQ6AKQu3P0ppQ+v40/hhQgEg4Nca1Z+nfZPAf26tHjn+F41Rly9nqSMOM8OpU/n/SvjO2fbuJPbpX23+2/cwQ/BW+glcb3u4ETnktvz/KviSQKkjbemTXdDSFj8j4s0xtxokbySM96ZuY96RnwMZqJpRjYDz7Uz5SLlJ6DoPOnkZVQgqcZC/ka+xv2OPgPdeCNCPi/wAR2pTUNUt4/LhfrBACGVD9TkmvPf2Of2cl8VTxfErxXZb7GKf/AIl9vIvM8qnIY+qDt619e2to1qgCoBgYA9vSuebsfonDWUOklWmSlm7jJNCtkdc5/WqeoalFYWr3ckgVEUs7HsB3+lfL+v8A/BWj9k/w98WJ/hRqPim4Jin8q41y0gLafHcbgvku4O48gfOBtGetZe1prc+1rYyhhfjdj6ocAj5u3rXj37RX7M+g/FuBr+3UWerwJ/ouoBRiT/pm9eheDPGWmeNLSHWtB1NLu0mhDxSwyBo2jJ4cHOGyOmK3jAJUIYZ9jzzXgZ/w9gOIMDKlVV7nfluZTpVVVos/Njx/8P8AxL8OtYk8O+JNKe2uovvE5KypnHmIe9YCIpRi33sda/Qj43/Arw98W/DUmkalEIrmIbrK+VRvhfHAPqp9K+FviZ8MfF3wr8ST+GvEdgYnQkiUD5Jlzw6Hvn07V/EfiL4Y4zIcTKvQV4H7FkHEdLGQVOo9TmGYnJz9KYZCBwcAKQOe1K7/AClc8+tR4cjrX47g8RWwGJVSLs0z7N06dajy9GfX37GH7TkGvWlr8LPFV8Y9Qs4dunyyt/x9Qg8Lkn745/CvaPi78Z/D/wAMfBt14g1a+UlY9sMe8bpHIICj8a/N3TdSvtI1OLWNOu3gntJQ8TxsQVb14PPfit7xf8T/ABz8RL2O88aa/JdLCuIoQcInvgdTX9HZT4xTwnD0sNK/PbQ/PcXwb7TH+1j8PYf418V6p478T3/ijXZj51/cebKpJ+UD7sY9gKwnk2g59OoqzDtWPCLkdea6f4MfCTWfi94+g8LWsLi2dhJeXPaGIHDZ9z0FfjuCoZjxlnrT95yZ9PWqUMowGmlju/2L/gJqHxG8YQ+L/EumY0XTJ/MXzAf9MnH3Vwesa5z7n6V9zWln5EYjWEAAYFY3w/8ABejeBfDtp4f0a0WG2tIVjVAMY9c/pXRPKsabyRjGa/uXw+4Rw/DmUR5l75+NZ3mlXHYlyb0K99e22n2hu7iZVRUyWJx0Ffnv/wAFA/22pPHN7ffBT4b6gI9Mgfbqd/FJ8164PMKYxiPnk9zkV61/wUS/agn8AaG/w58JakE1DUF2ztG43W8R4Jx6t2r89IYXuLk3M2S5ySSST+ddfE+fKlD2UT4HNMwUFyRZd0xBHGuExhcY9Paroi3DgcVDZxBk2jt61atUZS4Ir8nrVvbSbZ8nUqObIDbEc8iqzw7Bxxg8VpkZ4NVpImbIJA965YNwlcmLs7nqn7Dfx2b4K/GG1bVr0x6TqTCx1IZ+VEY/JIeeofv2DV+odlcx39kLmIghhnIOa/FkH7NOzp1BPP8AOv0s/wCCeHxnl+K3wXt7PU9RabUtBBsLsu2WdcAwyH1LJwfdTX6rwhmvP+5kz7HJcXdcrZ9C2+7A3E1PUcSEr8opyuDxmv1GGq0PpW7jqKIM7m49xRVCG5OzINMY4GalJxyaQqD1FBCv0KTM8h4z+FOsXY8GfPPrSWind07021Uhwdp6+lBZe8wYxzSg9waRPuiloAROn40tFFABR9aKKACiilwc4oASilAJ6UlABRRQCQcigABIORRRB3owc4oAKVeo+tJS4PoaAFZ+wNIpAOTSUUGZJTI+GGBSYOM4o6UGhMgGM02m7vm+7QnX8KAHUYHoKKKAGt/tfpSjPc0tIGB6GgBaTKjjNLSP900AJu/2/wBKTJzmkBI6GigAooooAXax7UFSOSKUbl/hpOfvCgBKRz8tLTXz6UAV4jnGP71S7VxjFRRARnJBqbIxmuMBqAbGGO1LYgZJHpTKktgcsfauincBrSk//qpIMnBJ71EkpJw1T23f61oBLRRRQAAdhSjr1xSP/qWpkXLA0AT0dKAAOBSM23tQApIHWo2jHUmpKb9z3zQA2PcMClbOetO3j0NIOVO1aAGjr1xTkHeja/8Ae/WhQy9qAHDjiiimsxDcUAOwMYxTG5OfWkBwc0UAH0p0OA+aiXOeKeDnkUELcWJgDg+9Kjfw4oZTngUgDA5xQGqYpKhulOBBGRUeTnOaASDkUFj2bb2pnWiigAp0fejDbcYoVSDQA4ADoKD06ZprYXotJk+35UAJRRRQAUUUUAFRaYcR8+tS0UAFFFFABTISdwBPen0UAKTycVXg6H61PUDHJ60GZG33jS2S5L49aitxiU1ctyACaDQB7fzqIkBs+/FTR96XAHOKAIlAO5gM/PxUOw+YzKeh4qZCVQ4Pes/VdUtNK0+e+mlCJEGZ3PQYHJrkxc/Z03Ijn9w+Q/8Agqn8ZG0Hwtpvwi0icibW5/tF+qyENHaxnCg47O+frzXw/psfzBiOR0zXb/tU/Feb4z/HvX/GUExeyN59m09SeEt4QEXHszZb8a4ywQ7cluRX4dxTmXtsXyJ6HwWb4n2ldpPQ07dtqnBxUsYXymO/t0Jqrayk7u5FS+YVHA/KvkzxxznjFQyITkk0SXBA5qL7UH+UZqW7rQtXsQXYj2MRyecDFZDx+TteL5Cg+Ug4x71rzMGyqis+4QHI21vga9TDSub0ajpO6P0A/wCCeP7Wg+Ivh9Phb431Pdq+nW6tbSuRm7tPuhz6uCMGvrNbiJkDiQY7mvxd+HPjfxF8NvGVn408NXjQ32nXXn253cFcfNGeejDI9jX6u/s5fGjQ/jf8NNN8ZaFIoSaLbcQFwWglGMxt3znOK/ZOFs89vTVJn2mV4+OIpezkdf4h8N6f4n0W80PUrdZIriN45Vburd6/Pr43/Cq/+FPja78OzwsLcMWtZSOHj7EV+jaKxUE15N+1L8DLP4peD7iW1Qf2jYxF7GTZn5sZKH1z2r9EpyTWh5fEeUwxeH5oLVHwRGzrgnoenvVm3lYuOe+arXEN1YXU2nX0DJNHIUdG4KOONpqaJisYJ5OOtPlZ+S1IfV6nLM6Hwbf/AGXULS4lPCzxk/QOK/SPwxPFd6LBLA4IaBHQj3Awf0r8x9OuzGQOmK+4f2O/ivB46+HcWiXV1m/0pfs86k/MV/gb3omuaJ9/wfjKUHKHc9pBBwPWkRkhVgx46/hR84hDSHBA5rgfjJ8W9I+GHhi41jU7ncXYpawDrJIcgKM9s4rCFM+8xONpYWlzzPD/ANvb4iJd3Vl4CtJAfKdr27w33f4YwR78mvmVhkZznjvW74+8Xav4z8T3niLWLgyTXUpeQ7sqvpGPYCudyxZixJGa3ulofjec4369ipTRDOwU5Fegfs5fBC6+MXixbCWOVdPs5Fkv5wDxGTynuWzj2Fct4E8A6/8AETxNa+GNDtTJdXMxTcfuhc8u3+wB1PqK++/gX8IdH+D/AINtvD1hbDftDXU/8UspABY+3pSlKyPS4dyh4qtzzWh1vhLw7p/hnSLbSLCzSGC1gWKGCMfLGgAAAq9eSRxx+ZuGMdSe1K04X5lOf614j+21+1R4f/Za+DOp+PdTMct//wAe2j2DSY+13jg+Wh/6ZgDe57IrVzzlc/TKk6eX4byR8zf8Fdv29Lr4WaTP+z58LtUMeu6pbj+1ruE/NZWzZHlgjo0gJPsK/Kn7TOlyLlXKt2OScV0PxF8f+Jvin451Hxz4x1Nr3U9UuXubmeT+NmbLY5wAARsA7cVjNbh+W79/WvnsZiLzsj8yzbOp4is+x9Z/8E2P+CjGq/s4anF8PfiRcz3PhG4mJhbO6TSy3G9QSS8Zzkr/AA8mv2C8CeM/C3j7w/ZeJPCmpwXNld2qzW89rJmN4j0IPQg1/OdApgbfG2MHqK+rv+Ccv/BR7XP2Y/GA+HXxAv5LrwXeTgSOzFm0qd/+Wsf9+LnDIOF6jvXVgcbze5I78i4gdKfJN6H7QCBEUxIpx/tHNcF8c/gZ4f8Ai74Xm0i/gWK6jUmyvQPmibGB+HtXR+CPGmi+N9DtPEugagk9ndRrNHJFIGRkbo2ehzwa32w44Gf60ZxkeAzzByo1o3TP03A5hOElUps/Lf4leAfEPw18XXHhHxJp7RXNoTnPCypnAkB75rBVy2Pm5Pfsa/QH9qj9nfS/jL4bc2UIh1iyQnT73aPn4/1ZPfNfA+u6DrXhTWbjQ/EWnyW13bS+XNbshG0+vv0Nfwr4k+HeJ4fzGdSjH93qftvDPEFLFYdQm/eKrHDGljuCGAPYjjPWmsD0U1DuKsWwSPavyGhCpOpyLqfWyqpK72NrShcahdG1tImllLqkaRrkyOw+VQPrX3p+yt8DE+E/guNtVhX+1tRxNfdP3ZOCIge4H868C/YL+A9x4i8Rx/FLxNZFrTTZG/spJQcSXBzl8dwAePevtSOIqgiHGOhr+w/BvgKOEoRx1aPvPY/I+K87dfEOjB6IeYlZSrdO4I615z+0n8ddB+A3w91DxXrU481YttpCW/1srKQifTI59q7zU9Sg02ykuLmTCxqSxJ9s1+Yf7d37RM3xn+KVzpehasz6Ro05gtVVwUllBxJL7qc7R6YzX7pnGY08voOK3PzHMcYqVJ9zyb4geP8AxJ8S/Fd94v8AE140t1d3LSyKWztJIIQf7I7e9ZtqoZeT171Ut+Blc9Mc/Srdsvy7RX4pj8dVx1ZykfBYis6s9S7aRgElWzmrlsOWyepqpZkN05qzE+0nB71wJWONKwojOWbPAPSo3iIHzVYSQMhGT17imOAVzUOJtT1Mq8t8RuceuK9m/wCCdXx1b4Q/HKDQNZvTHpPiACxuyx4jlLboJOv9/KewevIb2I+XkDr2rPj86yu49Qs5TFPFIGjdeGU8YI/HFexkmLqYXGxa2PQy/EfV62p+2djdpNbiVMDI/I4qWIqIcA5z0ryr9kj4rwfGD4LaF40afNw9oIr5C2Ss6YRwfc4B/GvUbYY43d6/esuxH1nDxnE/QqElOmmicHIzTUJx/KlPC8Gm20mMrivWNRQOoxSDc3GaSLIZ8evFR1lTbSAalvsbduPWroVfSmUoODmtTMgC4PBk/KpqKKDQKKKKACiiigAoBxyKKKAJF6D6U1k7gUiuR1pASOhoFZi8g80ZPqafTGGDQCv1EBxyKUHBzSUUDAADoKkqJTkUtBmH0opE6UtAElMtwPmOKEJzgUAkdKCofEKBjjHahWUD0pR0HFGX9BQUL36fjQMdqQAYxQAQOTQAtNKf3TTqTevrQAoAHAprntmnZB6GmkfdNBKb6jaKKI/kNBQoUtQy7aIpe2PwpWDN2oAaCQciijpRQAVAgY461PTX6/hQBVJOX57UUUoAJxmuSzAkT7wp9ocFxntTE65B6U+14DH1rpgBW2L6VLajA/Gm+X70+2GenrVAWApPIo/i+b8aIifJ3e/ekBIORQA3/lnT4MeUMUMMHFJCeMUAPPHIx+NIxJO0UD5RytCNu70ACn+E07A9BSYOc54pQABgUAGBjFIoIHNLRQAAAdKKKKAG/c9800kk5NOYsvem0AFFFES7W60AOj70eX706igS2G/vKRRk9aeBmYg03o9Ax1MU/vTT6Y2dxzQTHYiqaEYGcdqhwT0FSRDAORQUSUVHFPx1zTvM56UE8oNu/Cm0qliPlpSh7UFDaKCCDg0UAFFFFABRRRQAUUuD6GjY3pQAlBOOTRSPnbxQZjDOM8jio88yE+2KiaV8kcUili3f3qYgLGqrOzdBUyvgcIajwfQ0+mnc0JYJM077wx71DHu8r5fWpELbKHsBBMqxkkHpXgn7f/xrT4U/A6/jsrkR32pyfYbMgkHLKAxH4Zr3mcs3Oa/Pj/grR4xfU/if4c8D20p2aZYTX1wgbgyOQiZ/DNfMcR4v6tgJy8jzcdW9hh5s+W7VWkZnY8mr1rHgkD86q2EbBAG64q5CHVuB9a/n/EVvrNZzZ+cSqe1qNsmhHklgB1p3nAccE/WlQDGWHHevQvgX+y74++PuomHQZ0tLGBwLjU549yAkj5FUf6wj9P1rXB4Orjq/s6ZrhqM8RW5YnnXnIycqM+gqoZP3jFQPoK/QH4d/8Ew/g5piw3Pju51LWrlFG9J7gRQk+mxOo+pr0Vf2Ff2bUsxbwfCvSgQuAWDdu2c819pheC8TKFz6Olk0pQPywluHDMCDgHkkcCoZZAxyTnPf1r9JfG3/AATe+BXiSyeLS/Dc+iz4G26067wVPrtbIP418jftL/sOeOvgPKuo2N22q6MzHdqKriZOmEkUfL/wIYrjzDhbF4SDkclfKakFoeD3EuJCq9yM17j+wL+05J8DPiha+GPEequug6zcpBel2yIJW/1c3Xu3yH0HNeGzRGOR0xyrENz3FR2cQhna6Xhmzzk9P8ivNyfG1cuxOpw4KtUweIsz9wtMvbe+tUuUddrYHBBH0qe9SOaExOO2BXzF/wAE7P2il+LPgBfC3iG8J1jQYER1kY/v7YYEcw7luMN/9evpxsSRAk5BHWv3PK8x+tUFJH6Bh5QxGHv3PjL9t/4BL4V1j/haPhuyJsrw7dQiReIpO0nHqc5r59jfK9ee/wBa/TLx14S0vxpoF14a1i1EkE9u0UoYdiOo9x1r88Pi18MdX+Evjm+8I6jA3lxyEwXBHDwkjYw9T1Br6GlL2isfmfFOSqlU9rBbnPRMSpKnnHBrsvg18VNb+FXimDxBpzs0YAS7i3f6xO569a420JYbTVq3wpyvWh36HyeBxdXBVeaB9y/8Nc/DyPwP/wAJNJr6s/lYWwUgzl8cLt7/AFr5b+KnxT1/4o+IJNY1a4MCKD9mslfKRRk/d9z71xMU5EeQ2Md+9SK52Bc+4p2R7OOz7FYylysgkIQeWBgY4HpVYRGWTy0PXoRVlxuYgmvWP2TfgS/xE8bReI9btSdK06YNIrDK3MoIKgegHf6VDV2edlWCq4vEqJ7N+xl8Ap/BOgJ441y02alqQUxxOPmgtuoX6sea+gChVeF/SjTreO2gWKJQAowMdh6U+5eOFCzMAMZrKrLsftGV4KngcMkcl8SPiF4d+Gfg7UvG3ivUks9O0qzkuLy5mb5URFyzfkMDHevw9/bb/bK8YfthfE648SXt1Jb6HYTvHoGkFxiG1YsA5wRmRyMsfQ46CvqH/gtj+2G+uaif2XfA+rA21jPHN4oeKXmWXJaK147AfM3boDX55WUOHBUnPY15GMxXs1Y+D4mzrlm6MHoSxxMBnJyRTi+Tg4JqzHasw4TNXNG8BeO/Fcty3hTwhqmom1QSXP8AZ1q0ogQ9GYqSBkDpXhtOq7nwcI1sS7RMqSQEYHX2qBl8n95GduOhBqSW3vLSaSO+hdJEbbIsikMpHVWBHBFNL7lI70oxcJHLN18HVuz7Z/4Jef8ABRe4+CGo2fwW+LmsGXwvqF5ssrx2JfSWPALk8GNiQB/dzX646Xrdlq2nx39nMkkcqBkaN9wIIyDn3r+bazna2cPG2DX6Mf8ABKX/AIKJ3FncWH7OHxb1pngmzF4Z1a5l3Mrf8+shPUnqhPbivfweOv7sz9D4Z4ic37Kr8j9NXQSLtcA5HINfPv7Yn7Nsfj7SZPFXhexUavZQlmKqP9Iix933Yc175ZXS3ECyj+7zzzS30CTQ/vcY6g+leLxXw3huI8slSkte5+r5VmNXC1VVhsflU0DW0zwzqQYmKEMDkkHBH1zmtv4RfDvWfit8RLTwPosBaKebfcT44igBwzH39K91/ay/ZZ1E+K5vHngzS5pra+cNeWNnDueCX+8qr1Dd/SvVf2Rf2eY/hLoX9r63Yj+2NSj33UgT/VJwViz6+v1r+V8o8JcTT4nftV+7T/U/S8ZxPSq5clF+80er/DjwVpfgbwtZ+GtHg8u3soljRMYPA+Y/jXQTyCNNzHgjINQRuwBAOM9SPTvXNfFz4maB8LPA+pePPEl4IrSwtGkmDNw2BhQO+WI2/ia/rfAUcPlOXKjHTlR+WYyvzzc2eCf8FF/2k2+F/gOTwB4d1Ex61rrFPMVzut7fbtZ/x5A9M1+c4m82bB67cDk9PT/PrXY/Gz4s6/8AGr4h6l4+8RzNi7dmt7YtxBDn5Yx+HNccsTM2ccdq/KOJs2li8S1B6HwuYYx1atkSQ5QnJ79av20YIBx16e9dD8LPgx42+KOuxeHvCljPcXcxG4AbQo4G4kjCp6nr6V9h/Bb/AIJd+GdLii1f4p6++pTFRv0mzTy4FbjgyE7pB+VcGV5FisdHmMcPldXEatHxJCuBnIB78irMJIG7HB7+tfp3YfsM/s6WdmIR8MdKOFH+thLn6ZJ5rmPHX/BOP4H+KbYyaX4fm0O4CgR3GlTYC+7Icq1fQVODcUqd0dzyKVj88YZQVYHp2pCQ2Ste5ftF/sL+P/glYP4n0Wdda0WMEzXUCbZYuc5kX6dxxXhyKvlggdq+Sx2V18BLlqKx5FbBVMJJ8xXlGWOPwrOuYTvMuPetNgCMmqtwhK8jtXn0punK6OeM7SPrP/glT8U3s9Y1n4U3t2wWZRfWaMeA6nEgH14P419325DrlTx6ivyX/ZK8by/Df48eH9eeYrAb1I7nB4Mc48t+/Y7DX6v6NeLPaqx446V+1cIY32uDUWfe5RVc8Oi/BGsUbSfWo4cgjFTLjHFIAucn1r7hO56wLherUuDtxjtSgADAoosgEt+HkIbvS1HAwMzgf3qkpkQ2CiiigsKKZ5vuKfQAUUUUAFFFFABTkPamjr1xQCR0NAElNk7U7hRTWZSPWgBtR1JUdADogdhG8cn1pArdhTUQ56Z9Kkj46jvQALkDk0vm7uKQj5cCmgHI470ASAt0Bo5x0/Gkp8P8X0oAaWJ6mjJzmjJzmgDJxmsy07juFFG8ehpG+792m1oQOUMRndRwje1AP8K/maJO1AAp/hNOowM5ooE1cb9/2xSEEdadnA+Y0jfe+9QMTJ9TSUoBPQVFQBJRUcfzjNSUAFI/3TS0jkYwaAKJyG60Jj1/Whskk4pqlicbaAJIQVGIcmrCsBimW4NAznigAp0WVPAptRxydjQBbQ8YpajgyVHPai0ADNgfTNAEqDKHjtTYyQMj1pcDy+KIMZ5oAKcG7KtIFJ5FEfQZWgT2H0UUUDCiiigAoJAGTRTZO1ABuXp2pGxnilI3fMtNGc8UAGCeacv+5QqdyKU/eFADKKKE+5+NBmHFFNVMOW/KnwY2/jzQaCowA5NKBhcUwAngVJQAzYQAKTy2Pc1JSZb+7+tBnyDI4+KRQonI9O9SDoKZQXTFT7o/3qeOnTFMhORyaVX7E0DEI2nANJSkk9aQZzxQAUUUUAFFFFAATk5ooooMwpkxwB9afTS6ntSewFOUfNketSWQCtID602mxjrg9TSWu41uWOCcbc/So8lTjyj9ansoyZH3dM8UfZmHU/lQmWNQYUcU4ZxxmmhAOhP50ebsLk+tN7DSuyvfSrBblnPbOa/Kb9sLxsPiH+0f4j1XJMUF6LOEluPLjIXj2LZ/I1+l3xh8ZWvhLwBqviSaXCWdhJMT6bYyf8K/JHUNQk1zWrrUbqUmSd97N6s0hc/qa/NONMWoUHBnzOeVeWDQtra4TkVPHGANwqSFRt+UflThAM7lB+lfjis9j4vRkbcDB719V/8ABND42abpGsah8KvEM6wNd3Hn6S8rYzJ0dBz1YYIr5WjReWZuh4pdO1DWNFvBrOl3j281u4e2lhkw6uMYYHrkdq+i4exlPA4vnkejlteOHq8zP2RtTGygqQQB1qYkhpBk9K+S/wBj39vTTfGmnQeCPivqEVjrMCiOG7cgR3iDpk5+Vz+tfVdjqen31qtzb3CsrrnIcH9e9fteW5jhcTTvGR95hsVSnSvEmSMFApHUdKw/F/gvS/Gehz6JrdjHcQXCFJYnAw6nitqS+gUcsPzrnfGfxU8C/D/TW1Dxj4nsrCKNSS91cKhx7Dqa3xlXAVKfLUkROdKS1PzO/bI/ZS1f9n7xmdXtEa40HVJ2GnTAf6psgmJgO/XBrxhYsMAR3GMV9T/t1fte+GfjZbL4B8DWEVxpkF2s8mpTAh968Dyhjpg9TXzEkTM+WUD2r8Wz+OGp4t+xeh8Pmapxr3gzuP2efi3r3wR8d6d410eZv9DmJuolPE9u3+sjPr3I9MV+sfw68aaP498I6d4r0KZJrO/tklgKtnKnHU+o5B+lfjZHJ5K4B6dPavtD/gl5+0Y0l3cfAnX744KvdaG0j/cI/wBbAPcj51Hsa+l4Qzdqfs5M97IsXze42fbhiyCCMnJ6968P/bM+DEfjvwBN4l0m236jpMbOoRctJF/Enua9zgeNgNp7cZqvqNtDdW7wNGuGBBHY+tfruHqcy5kepmWEjjcPJM/La1ZI2Kn06VZtpFdM5GCa9B/aq+DjfCjx7PdaXaldL1SRp7IgcRSZy8f9R7V5rbH90Y1bkdCa7rJxufi+Pwc8LXlGXQt27YDYPenCbgrnn61BEWPBfk04QyGTy/UcH+tYttM46V5SSRt+D/DGq+MdZtNC0WB5ri7lEcQVc8k4yfYd6++fg98NLL4Z+D9O8L2CDFnATO+OZZW+8fzryX9iX4KLoWkN8Q9asc3Uy7LNHHzQxnBLD619GBGVdoUGspzaP1LhvKFQoe1lux6yCGEEn+HnH0r53/4KAftoaJ+yR8H73xGlzHNruolrbw9p8r/6y4YEByO8Uf3mP4V6/wDEbx5ovw/8I33ivxFqK2tlp9pJNdXMxwEVFJZj7DtX4aftw/tQa9+1d8bb3xxdXUi6PaStbaFp7tlYLTsRj+Jz87fgO1efWrqmdufZtHCYfli7M8i8ReJde8ZeIdQ8V+KNUmvLy9uZLq6uJ2y80shzI5+ucjsPypbWPimxWnGT6f0qxDEycivBxFT2rPxzG4meJq8zNnRLNbmVU2E/Qda/Zf8A4J7fsveH/g/+z3oxvNFRtX1yFb/U5ZEy2+QBlQn+6q4Ar8i/2e9Kh8U/Frwz4WnQkX/iO1t3H+y0g/pmv3+8L2VvpulQWUCBVggWOMDso4/pXVl9FSnqfe8JZbSrR52fOP7VH/BNH4E/tFWt1qz+HY9G8QPG3k61pkYRyxHWRcbZB65Ga/JX9qv9k/4ofsq+OJfCHjrRSIJWL6ZrMCMbbUIgeqcZWTAzt/Kv6CxbI4G9evXNeX/tE/s5+AP2gvAeo/D/AOJPhuO7sbtGEMwwJIJCNqzRt1VxntXoVsFCWqPcznhrDYik3FWZ/PQ07kDa341PpOvaxomqQ6tp140Ulu6vG6NgxyKRtkBz1H9K739p/wDZ71r9m74va18MNcmM5sLnbaT+Xs86Bj+7kA9SAcj1rztbdyQSe4PFeZODpSPy2pSq5ViuU/ZH/gl//wAFBdJ/aO8Kw/DDxverbeLtJsw8m9gv9o244EqZ6vxlh6GvspWSQArggjgg8EV/On8IPiH4r+E3i6x8d+FNcfTtV0u8SaxnjHKuAOSP4lcZVlPAGDX7k/sY/tK6V+1B8E9J+JOnyLDNK32fVrFXDG3uU/1kefqAy+xNepgcavgkfqXDucfWoKnJ6nsDWcTHeEGexApFgZPlUYFToxYdacR6itHhKKnzpan2vO+UpvOkKnd/D6V+ef8AwUj/AGjLrx547f4QeGr8No2kXAkvhHJxc3g52Z/uKCePXNfVn7ZHx6h+BPwo1HXo7lTqV2/2bSYi2CJnXA+oUZY1+Wd7ql1req3OqajctJLL5jNIxyWkcjLE+9fB8U5usPB04PVnz2a4vkhyoIgoYSLzg5HvW38O/A2r+OfFll4U0LTHurq/uFihiXJG9h94/wCwOSaw1ZUXrn616L+zL8c7T4E/Fay8cX+gjUYLeN4pkRsSRB/+WiepGfu18BlUKWKxP70+dwcIVa3vH6K/szfs3aB8DfCNtYR2iTahMFa/uwBukcjlQf7gPQV64tvt429Ohryv4KftdfBj41W6f8Ib4rhNzsHmWNz+7mjP90oxz+Rr1OHUbOSPekq8jPWv2PKXl9HD8sWfa4d0KcLRJoslcZzUu8bRgjp1zVeK7tkjxkEfWvL/AI9/tUfD/wCBmkSTa3qwu9Qb/j20q3dTKxPTOPur7nmvQxGY4bD0bykaTxNKELs4z9v/AOKNp8P/AIRX+kQMv2zWlWzhi3kHaeZHx6YAGa/OtVLtgYwema9A+Ofx28V/H3xXL4n8RHy0jQpbWiNiOGLj5Uz97PX61w6QlYySe1fjnFGZ08ZXThqkfE5rilXqe7sVpItowT2qvNFkY/WrIjIHLfTmmugA6V8YqiueMULWee2uoLvT5WSUMTkdUYYwR+IFfrX8CvGaeOvhhoHi5Gz9t0m3lPOcO0e18++RzX5KFvKk8wdc55r9G/8Agmr4wh8S/s7WemvJl9G1KezYHqF3CRP0f9K/SuCsdzVfZeh9bw5iHJyps+joCTCD3xUlJaqQvI/CiEfM4I9a/YYM+rF6UgYHpSPw2aaCQcimBJgZzikj+6aFORRF9+THpQAoODmiiigCAzRjg2hqeiigAoopRjuaAFV+xNDr/FmnUhOBkUAIv+/Tec0AkHIp3me1ADaKUqR1FJQAseSuGFRp96n1FAcKMGgCeIfJg0KVHQ0qtuFG3/aP50ExIwT5hYU5PvCnFcjGaRf9+gadxu/DuD6cUgY7QKlqOIDGMZ+tAxR8ucetK/X8KF54I6mhzz9KDOAoORk00gqaVdu3n8aaevXNBoFOX5myabSqcGgB+B6CigEEZFNZmB9KAEJyc0g69cUUuT6mgBASOlRAGTjHFTKueTRtYdqAEoyM4zRSeUMZJoATzPakUEqaSnp0/GgCLb+7YAd6iQZYCnSAk8U3a3pWENikycDsBSQRgA59aYOnNLbsQh55zW0CQfGeKgTlgp9aseX71EYRnIPemBYRTFjPOKW16/jQqf3hSWxxkigCUllGP1psB4IpVGTSAAdBQA+Ahd/bmmxEEUkB5IpYtvagWjQ+k3r60P8AdNJu/wBv9KBjsgdTTd2P4s/hQr9iaGYEcGgBcnsKRSzd6FfsTQv+1+tADgABgUgABzS03d83tQA7pQAAMCkByM4oyfX9KABe/wBaZTwOoI71FH3oMx67v4aYHI6nt2pTjs360p+6fpQX0Ft/60p/ixSQHHSnKOTkd6BRFHTpiigYxxQSR0GaCgooo69RQAEZGKapIiBp1Mf7xoASiigHBzQAUUUUANiH7xz7U4A9h9KKn2gA4oMYlfB80gUtIvf60Oflx70FBvX1paKba48snHfvS6gVT0PNMtoMng96fUtqAOKFsaEnAHvTd49DSedj7ufyp4znp+lMCNjk5pMhI92c+9TKv94VG8QiiYkds81LegHgn7e/iWTw7+zt4gkgYI9zCtunOPv7Af0r81NNQvOzkcljzX3x/wAFP9ejt/g9a6RbuAbzV4lIJ5IWMNXwhpsLKM7a/GeNqrnV5T4zPZpysXrRSu4AcVPGNq5IHSi2jYxsxXkGnsuRwO1fnMFY+YgUYY/nk570mHHSrEcZG/jvTHjI5C0SbWxavcrfNCAYjtYHgjtXa+EP2o/jt8PrCPTfC/xC1KC3jGEhkkWZVHtvGf1rjZXJXlPrVW4RymO1dODzfF4bSDZ0QxuIoq0D0fxF+3H+07rNq9jN8VL2FG4JtYY42x6bsV5hq3jjxJ4pvPtviPWL28uB1mvbhpWP4sT+lO/si5vcRxQs2TjhSc+gruPBH7IPx/8AH4jl8O/DLUmhlAIuLr9ymD3y3avo8PWznHx927OmE8yrrc8+SZpF3MSfQk0qMANgI49690H/AATf/aetrXzT4VtXOM+Wmox7vpXB/EX9mj43/DGOSfxZ8P8AVLeBD81zHGssf13L0Fc9bJM01lOJlLAYt6yRwNzcBMgdj2p3gn4i+IPhj470/wAa+Hb94byxnhuLd1P3ZFyfXnd90j0NUblpgcPk56Hnms25j3OWHPPBrkwdStluIvLcyw8quDr3P2d+Anxb0H4y/DTTfiJoLjytSs1kaEMCYZON8Z9wa7V+U2ua/OX/AIJhftDT+CvHCfCDXNQP9m6w3+hNLJ8sNyMnA/3x+tfozGySR5Q5B6Gv3Lh/MVjMMmj9DwNeNfCnlH7TPwiPxN+HVzo8UardxMbnT5sZKSKBlf8AgQJFfBj28+n3c+m3kXlzQSMssbHlSDg1+o95aLcRtG4BO04Jr4H/AGxfhZc/D/4wXOsWMBFpqsX2mA9FV/41HuQK+qoz6M+E4vy/lh7WCPM4CrIGU5U8g+1eq/sufCIfFDx3HDf27tZacBc3UjDhsn5I/pXlWl20t7LFa2sbs0jBFRR1J4X8zxX3t+zJ8JU+Ffw9S3uoB9uux9ovjjBDFRhB6gZ/SnUtc8DhnLfrNbnmj0vw3olro1hHZ2cYSNEChB0AAAwPbir1zJDBCZXYKAuSTUcE5SP5uOPzrwn9vD9rTw5+yp8FdU8e3kiSapcP9j0LT5JMfab1wRGCP7i43sewBriqzVrn6tVq08vwlz5C/wCC1P7YH2maP9mvwRqIMaOk/imeGUZ3HmG1OPUfO3tgV+ddtbKy5J55q34x8Za94+8TXninxJrMt1fajdPc308r5Mrycs3X++Rj0BqvZHPyn05FfOYqs6k2z8bz7MZYyve+g9IQBnHA4pQgAGKtQQCQMMfQYphhHBA5rhbPmW9TX+EfiwfD/wCKPhzxm5ymk65Z3sgP92OYbv8Ax2v6B/BPiKy8VeGLHXNOnVoLy0SWJ0YEFX2kH8QcfnX87Ugw/A5r9Ov+CO/7aq+L/DMH7NXxB1YDUtLiMmgzyyDfd2wPMB7l1PzD1X6V6uXVFzWP0TgrMoU6kqM36H6I4+QY7VDdReYhAWn2syyIMEdKfkSRkqcjFe+mmfqUuWrRZ+XX/Bd/4RafaS+E/i1p1qqTXE82m3jKOW2qJEJ9+DX5wqhBzmv1w/4LjWsFz+znoW8ZdfFwVTjn/j3kz/KvyaltNrbTXgZhaNQ/GeLKUYY1NdULGQoAzxjp7V+k/wDwQcl8USaT47jmkl/saO8svswZvl+2bH80r/2z2A++K/ODw5ol/r2rW+iaXavPPd3KpBCvLPI7AKoHpu/rX7h/sDfs4xfs2/AHR/A0yqdRaNrrVJB/HcShWk57jACj2FTgafPUUux2cH0Kkq7n0R73aggAAcUmo3cdjaPNIRgLkc9eKW2ZlUHgn+deGft2fHmP4O/By8awvwur6xK1npgDfMjMMM+PRV7+pruzDFxwuGlJn6nWqrD4bmZ8S/8ABQX4+3Hxc+MV5oGl3ok0jQw1taKG4acNmWYEdR/APpXhMEpYA559asaojXUzSsSzHPznPPc9fU5P41Q/eI3lpznoK/Bs2xVXMsa+U+BxWJq4utoXt+V60xgc4BHXIroPBnws8f8AjeRIvDfhu/vC2Bi1ty3U/p9a9b8Pf8E4v2j9ft4520KK1SRQf9OvVUj6hRkU8LlGY35oG1PA4xaxPCbC/v8AS9QS+029lhni5jlim8tk9wynOa9W8HftuftIeE7SLS7L4n38sCrhVuoopyO3Vhmut17/AIJkftH6RZNd2NlpV6QcmC3vn3n6buK8Y8b/AAs+IPw013+xvGegXlhMc/ubqI/Pg9Ubo30r0+bOMFG+tjpX1+hG7PT9Z/bV/aH8T2n2DUPifqMcTjn7KkcOfxXmuCvPEOpa5fSX2rajNcTtktNNIXZs+pJyfp0rBtCeIz+Iq/Eo3cCvJxeZYyq7VJHnVsbiJ6SZoQ4ZQ35U8jIxRp0fmQ/N29ql8kgH+VeRVm5o5Iu5VaIAf0qKRD5RI9PWrEmdvFUZO+a5hFK4DbCSM19of8EiPERuLfxf4akb/UT2V3GpbP3leNjj/gIr40l3CM7RkV9K/wDBKXVbiy+Ous6fHIVhvfDR3x56tHMpB/JjX1vB9bkzD1PbyCp7PFH6JKoYY9+MU9gAvSmW+HAAFOYkcE1++UHzUrn3id1ca44zTVODnNOJUjrTK1jsMW3+Z3x6021J3SNTrc/PIaWEYlk49P5VRENh3WigHHIpDKvoaCxaKIv3vSigAoBI5FFFADlYAYptFA69cUAKq7u9LH3oCsDnIpwAHQUAIAQOTSMpLfWnUUCshhIPQYppGMAetOIAPBpKBhRRRQBIvQfSo6BjPJpYOh+tAkrCA4OaW26MPalwcniod7x/6rIP0oGSg8ikpkcpc4K4p9AqYp+6KSiigYUU3y/ekUgqeaAJPm/vfrSAkHIpUP7qkHXrigB21/7360bX/vfrTgABgUUAAAHQUUdKaXyOKABl9FpHyAKSKfyx0psTEliDxQA2nIcqcVFhj2/Snx8blxQAzI3Z7ZpE+ZW5+lEZ7kU1hySDWNPRgELyY4BpYWw5HuaIH253HFOiXMrA+tbAPqOp3OFqJBzmgCam2fQ/SnUkI5zQBKAB0FV6sqRt2k0wp6GgBsHenp0/GkCgctRtZeaAHHPam/N/F0o8z2o/2/0oAdTZO1KGB6UtAEdBJPWlJJ60g69cUASDGOKKROn40uB6CgAoHTpijA9BTSSo20C1HZxzmog+eKcRtOAaSgYUA9waKSMlc0APQ/wmhOv4U1Dzye9KmAB+tACrxxnvQWAHy0L938aGUBfpQK6EDEdDSr/uVDz53Wpo+9Ax1Nk7UpO0ZAo3fLmgBlFFFABRSJ0/GloAdu75/DFJvb1pKUgg4NBmJRQSScmigBCcEUhJyOadTWHIxQBFbnBkNPh/1hK023z5r/WpqWiRoN/+KppJPWjOwZFV6LoCwD3BouVkSHg5OODmm27E4HtT3lVo8Zz6+1ZVbqGgHw5/wVc1k20vhbQAcC4ubq5YDsFWNP518lacUyOfxr6W/wCCrt2x+K3hq0aTcsegTSAE8DN0R/7KK+X9MuMsyqK/EeMZqOMsfC50/wDaDetUQo7A8k8A05QQOarWVz1GasROHBKnvXxSVzxHYayjODUbr1WpHIz1qJ2OeO9QSnYrsAByBx3NdN8Ifg54s+NfiuDwn4O0xppic3Ux/wBXCmceY5zwPT6VyTTORhj0PSvRf2Xv2h9T/Z8+IA14xefptygh1W1yP3sHBDD/AG1JPHpXp5JhaNXF/vdjty+FJ1bTeh9u/AP9in4c/Cuztr7UdKi1fVVCsbq5jBSNh/dB7e9e52unRRRhViChRhQB0/Kue+FfxO8L/E3w3beJPCupR3VrcRBhIjdOPun0I7iutjddvXiv3bKcFglhk4I+9w2Hw8ad4jBZR7fujOPSqGr+GdP1mxaz1CyjlRx8yuoI/XrWpuU96Cyjqa9aWDwtSNmjeVOm1ax8YftTf8E5ND8XafdeKfhdYx6bqwLyPAn+qvR6Y6Ixzgdq+Bte8Mar4Y1u68Pa9p8lteWMhiubeVSGVwcYP9K/b2VIpMhlDc8g18Z/8FJP2XNL1HS5fjv4YsAl5pzeRrKRp/r4D0l4/jUnr6V8FxPw5RnRdejujwMzyyDp+0itT4J8P65rHhnVk1jRr14Lq0nSW0mQ8o6EMrfXgj8a/Xn9lv426d8dfhLpHjuylCyy2oF3bq3+qnGA6EeuefxNfkPepDHKRx97setfVn/BKX433nh74jaj8IL+822mr23n2Cu3CXKHc2M93X+VeJwjmM6GJdGbOfJMUoScJM/RWLkMCe5615R+078Gn+K/gj7LYxL9vtT5tm5HJboV/EV6rZuksYcLgfX2p5SKXqAc9Pav1+nU5oKSPdx2X08fQcZdT5L/AGXv2SPFFj4tg8XePtMNrBZSBoLaQ5d5ARgnsV5OPpX1nBaJawiNVB2jAqWGONUCoOgpJ5Aib89q1dRtanLluVYfLaVomPr3iPTvD+mSajf3KpFFGWkkdsBcA5J9MYzX4f8A/BSn9rm9/am+Ot+dKvy/h7QLprTw/ErZDAN+9nGOvmNwPYV9y/8ABZP9qaT4PfCc/DTwpqxh1rxVuhBifD29p0mkx/tfdH4+lfkfDHmME/ex8vPQeleZja6jHlR8fxNnUk3QiW7dRtAX0457VpWG1EAX09aoQLlAxbH+1XafCf4GfF34x+J4fCvw58H3uqXbgGRIbcHZ0+Zjwsa+5NeIouoz4Glhq+LfLFXZlQRSS/MuTn0qWS2ZUx7V9wfBT/gi18atWWO/+I3i7RtGQgF7RI5L2YHjgkbE/LNZ37af/BMT/hnD4UXHxa0f4jpqdtprxpqVjcaYkT/OwAeJhk5BIHJ6Zp/UKrTkelPhzFww7qSjY+JJYvmOfzq94O8Y+KPhx4rtPG3hDUZ7W+0+7jmtJ7ZyGiZcANweepGPTg8GqqHduy27rz60y3RgCoHPPWsac3TlZHi4avUwNfnjuj9Y/wBhL/gqv4J+NL2nw6+Lmp2+j+IgixwXDEJb37dPlOcJKTnKHj0Jr7Zg1C2mgDQuCGXgg1/OVYo8Uu+GRUIbILHABHf619AfBj/gpZ+1l8E9Gj8MeGPiIL3T7cBIbPxBEt4kYHGFc4kA68ZIr3sNilJXmz9Iyvi6HsuWqfUf/BcX4hWEeneEfhejq0omutWnXfyFWPyU/NnJ/A1+Zl5HvlIJ/KvTvj/+0N8SP2kfGrfEP4m6qlzfyWyxPHDB5UccSkFUjjySBk5z1NedJCJZdrgnP8XYj14ry8ZN1qr5T5HN8Ss0zH3Nj6f/AOCSH7Pc3xa/aatfG+oWRfS/BkX22Zip2yXUgKW6HPXHzSf8BFfsZZ6ekUAgC4AUAe1fMv8AwSp/Z/tvg5+zLpF3qNkI9W8SM2q6gWXDDeMQofYRjP419URptACjPavXwNFUqOp+m8OZcsNg1bfqZ2p6jDpdjLdXEm1Y1JLE9MD/AOtX5d/tofHST4vfF6/kW5Z9L0qRrLTYwxKhQ3zuOf42yc9sV9tft3fGKT4T/BPVdStJdt1eyJZ2ihsHzJQQSPooY1+X4vZ7y5MsrFiTncc8+v618LxVmTT9imTneLUIKkXodKlv38qJcluhAz+NfUP7IX7A+o+Obi28bfELRjb6RA26KKZSJb5s9SDjEfp61l/8E9fglpXxS8ePqOu6d52n6JGJpfMGVllJwin1UDmv0a07TLewso7G3iVUjQBABjAAwAK4uHOHliJ+2nsycmyuE4e1kzA8H/Dnwx4P0xdM8PaNaWUUahVWKMA8cckda6JLCJIxiMcD0oWNAML+lSxbShXNfotPA4SlHl5T6aFCnHSwwWUEny7Bz61xXxh+A3gb4v8Ah6fw/wCMPD0VzC4/dzEAPG2MB0YcjHpXcx/c+X+dJPdxwRnewAVc5z04rPEYPBVKTUok1KNKUPePzG/aq/Yt8X/AKRNd0o/2hos03lxXqphoO4WZfXH8Q4rxmxXgMefrX1F/wUR/aiXxxrk/wZ8F3yfYNNfdq9wjg/aJQeIVx29T2xXy9aSEQ4c846/hX4lxLTwdPFuNE+FzaNGNW0DVsVC2749akkGVxVa0udsJBOM9RUpuFZcDrXy0Vbc8qBBJHjLVUuB+9wB+OKvSn5DVO4f5iQO9a8qKkVmfbvIH0r3b/gm/rIsf2mLGzUFftOn3kTHPB+RHH8q8Elk+Vjnsa9g/YAuWg/al8Mqr4Mr3CkZ6g2717vDdX2eZRXc9LKP97P1CQnZnPalLAKPpSQDdEGPp/SkJxn5ulf0DgX+6P0Cn8I6A/O2e/SkWIcEg0Kd8YGehqVMY4NdcNS27B5igOenNJGeMg0eWOxpbcYJFMgX6VDb/AOtkwe9SRj9647e9OAxwKDQKKKKACgdeuKKB164oAKkHTpio6koAKKB06YoPTpmgAAwMUUU12/hxQA047UU7cu3FMDn+6aAFooPXpigAngUALHGDyZqcAB0pFbsTTqAGlmH8NN3Kv3vMp5YA4NQMplPIzQZkkbwnOVPsTTmBJ4FMjhC9KmTGZOKAgRUVIYcnOajoNCJp+OlFocs/51E2T0BqWyHLADtQBNEMxfjQMk4BpsZIH40+PvQAqggc0tAGBiigBGbaKZTpO1NoAaEHc0inyWwO9Of7tMoAkppxHwT1HNREljgVIWJGDQBXYE5IPFLGxMWBSkcE/wBKLdRgk+tACIOM1PbqvmNx2FR47gcU9CTytAC5Oc0N940L1H1pDgRcntQZiIeP/r0tsMHHvSQKMc06AYBHvUS3NCVDgE0qfdFLgdMUVYBRRRQAU3d83tSDOetJQA77nvmm09On40hDBsigBuec07YT1am06PvQAqrtHNLRRQSlcQkDrSbc/wAOPxoJzznH4U6goaynO6owhByamwPQUUABIHWmEYOM0+igSViOlXqPrTk6fjTKBklIV54/lS0UExGFSOtCnBzSsncCmjr1xQUOJLfdOKbSq2ODSUAAJByKASOlFFABSJ0/GlooAUHBzSUUu1sZxQZgenX8KSl2nGcGkoAKR/umlooAZDKq/N5J+uKZ5yZ4NJ546Y/WkUfuCSKDQUyg8KetJTNpBwOvajbc+g/KpaASGQp0pBKC7YHfpQQY+cUhJ4BP1rFpuj5hJH53/wDBVi5uB8etGJyI/wDhExtGe/2p8182WF4eEXH1r7b/AOClf7P3i7x3Y6V8R/CunSX0ulWslteRRLl2jL7gw9/6V8MxW2qWkjWtxayxshw4kQqQfTmvxbijL8VWxjnbQ+EzfD1Z120bUF46sf3mSDxVqz1VkVwDyOKxYfMQbcMfepY7jYhHQk55r4yeExVM8KVCsnqbUdzlOufxpDPnhR1qhDeOVGOfpTzeEDO0H0rD2dXqRyyHyH5S1UbpiUJzj39Kle8WQ7BjJ96guDuBI5Na4ecqLuaUG4O56b+yz+1v43/Z08Ts5zfaJdNm50p5sMucZmjbor4P3e9fop8Df2o/hj8ctHXUvCfiOMyY/f2EoCTwH+66k5J9xX5IzW6FC2Bz04qbwx4o8S+D9Tj1Xw3rVzZXUZOy5t5SrL+IPP419vkvEtfDLkb0PocDm8qPuy2P2xgv7SQYSUEexp5lQw/eH1r8wPAP/BRv9ofwpBHZ6hqum6tHEuEbULFt5HbLIw3Guovf+CpPx3v7Yxabo/h22YjBdLWR2/De4FfbUuLaCj7x7cc6w1tz9BtV17StEtXvtVvo4I4uXldwoX3yeK+O/wBuD9ufwlf+E9Q+Evw2SPU572IwX1+zZihjPDYP8TV82/E39pP4ufFpSfG/jC/uI85FqsqxQj22R/1rz65Mkw+YjocYFfN55xd7ak6VLqebjs5jODjBmHPBvkyq5961Phb441D4X/EfRvHWmM6yaVqiTsVP3owQGH4qSPwqJrYFmI4x2qq1qpbcB9K+Hy/FVaGMVU8HDVvZ1lI/aPwF4msPFXhuz8QaZOGt7u1SeDaf4XAI/mRWzEMHHtXzP/wTP+Jy+L/gTb+Gr25LXGgTNZSFupiPzxH8QSPwr6YBUqCpzxX7zk2KWLwSlc/RMLUVSgmgiMgXB9a5X4lfEbQvh74T1Lxh4jvRa2Wn2ks9zPI2FVU/i/EcDHfNdY0m1OnOOK/M/wD4LhftS3Gl2Nh+zb4S1Ty5rxRfa+8UoyturERRH2dsn6Cu6vP2ULnmZvmUMDg5TPiD9tL9oTU/2lfjnr3xKv52NnPeLHplsXyLe0Q4jQDPc5f615XFNtG0HPvUUbvNMwkY9+ffPSp4LdQRtbA9a8CVZ1Z2Z+LV8VLH4nmfVn0B/wAE/wD9kLxN+1r8UotBtvMttD05EuNdvyhISMsQEXPBZ8DHoK/Z74Hfs+fDf4H+HIvCXgLwfBpdtCg3FIhvmbGNzv1Y8dzXgX/BHT4NQ/C79lXSfEVxYhL7xQ8up3L7eSjMEhT6BFB/GvsS3VGiBVMgjjNe1g6EFC/U/VeHcpw9PDqclqJBbxomEA9sV8jf8FkPEVtof7H+q2JlUNqWs2dvGueSd5Y/ov6V9dO8ccZAIwPSvzE/4LjfHKDVdf8ADvwN0a93GxMmq6miH7rMPKgQ/UeY34V0YiUYUWdPENSnQwM0ux+fsa5JYCnwx5H3adaxF1JH4Gp7e3ypJ4r5Vr3rn4dV96YyKP5ST+VI6qO9ShcLtzUckfckVfM0QlYhLPG+9Mgqflr0H9lL4Q3nxu+OXhn4dWkLPHqGqotzt52Qod8p+gUV5/ISTzX31/wRC+B0eo+JPEPxw1OA7bFV03SXZRxJIBJcMD7KEX8T61vhYupVsfS8O4X61jFdbH6S+FtBs9E0620zT4QlvaWwjijA+6qqFUe3ArVY+XHntinWYEQwUwc1l+Kdes9D0u61jUZxFa2tu8s7scBURNzH9K9zEVIYehzH7RQgsNhz4L/4Kx/Ekan8QdG+GlhMHisbd76+jVvuyuPLiH/fO4/jXyNBhSGzxXXfHL4l3PxZ+L2ufEC7mJGoXzyW6schIgdsaD22c/U1yttCHHTmvwviPMFicY3F9T4LM63t68pHv/7DP7W9t8AfFFzpXiqxV9G1GVftUsQzLbsOBL/tJ6qOlfo54G+Jvg/4g6LDr/g/xDb3lpNGHWWGQHg+o6j8a/G2CLyn3rx6EV1vw2+MXxD+FV6NT8D+KbnT2U9IpuD7lDkNXsZFxVHCU1Sm9j0sszX2MFB7H7Awyxklgwx25pRKiAjcOSSK/Ovw9/wU3+OWmRiHVbDQ9QIXiWazkjY/Uxvgn6Uuu/8ABT/493sbRaRo/h2zPTeLGWVh/wB9ygfpX1a41waWrPa/tmglufoBr3iiw8O6fJfajqccUMKZkaUgAD3PYV8W/tX/APBQXUtTlvvhx8J9SWOFk8ufXo2yz54ZIh2Xn759/Svnv4lftO/Gb4twmPx34zvJ4Sci0hEUMA/4BHjP4k1wRkLtuZufr0r5nOeMqldctLRM87F5u5QagOmnmnnM8js7FizFmycnrz3Jp0My7CM81FyBgE01vl4HAr4DEVZYmXN1Pma1SVXUtJeBRwaeupEKAD+lUYpVKZJHWkklwBtXj6VjGnVnsjmUKjND+1GzgNmo21DecsBWcZ2Pf6U0PMycAkduK2hg8VPZGsKNdrRE8smUPP416f8AsD6ikH7WPhKB5CWa5n7/APTBq8nEV5LHsCHJ6ZHvX0V/wTs/Zw8fX3x1sPilrWkXNppmjW0sy3NxGUE0zrsRFz94YOc19PkWWYmGNjOUdD1sqweKjiVNrQ/Si3cG1BH90VISIy+PrVeyDpCkbtk8Z9+KtEjGeK/b8JpRR+g0l7pDCCI8mlT98MAVIycfKKktwFrspjG1HHngGpKjJzyasCSiiigAooooAB164oopy/79ADacrerUitjg07BznPFACgYGKaTzjpTh06YoOccGgCPJznNOCqf4qG+X7tIp2tg0AKqsD6U7I9RTdyjoKQkkYoASmx+WDkE/nQzEHrRB2/CgB1EJwpopIz396AHZ4xj8aLV9ucetNccHAqMAjvQRHcnGQTz+dLkZxUUJG5hjtUidfwoLHZOcY/GmEY75p9NZO4FADSMjFQwnE5NTUUAFKpwc5qIDsBUlAEgzjmm/vKaCQcinKWbvQANu/Chd27n8acAOoFHToKAGswIqGpKjoAOOtN/+Jp0Z2DpSPyc+tADAcHNKij0p/lBT96iEYG6gBE/1W2iA/NgGlptuqjp2NAD8kcUqY8v8OabQp469qDMfCRtGMUsZAyT68UxQq8g/hTkPy1zJ3NB245zSh8Dmm0oBPSukB9FM+b+7+lPoAKKKKACiiigAooHTpigAdQKAAYxxRTY8bcinUCWwUUUUDCm7tvy4px6dM1HzmgBcn1NN+0HOe30pwJHQ1GWOeCaAHrNxgcURzAZBHaotq+lAAxgGgCa3favX86QSkmoNrY3ZpYFIZ80AWH+n402gHgfSildAAJByKKKKYBRRRQAUVHT06fjQAtKn3hSUq9R9aAHgAdKa4/iFOxzmmsSTtFBmRkZi/wA+tDNzwadKPkfcPTtVaT74NACRZDZAqwgIPIqGOXBkyO1TqSeooNA+X+7+lI278KdQ3Q/SgCnMGJ4qMjIxUpYkYNRH6UARPZwT23k3EKyL/dIzXLa/8Cvht4iZ7jU/AOj3Lucs01jHk/iK65UC4ZT1p8UgCsp9cV5uKwuDqP8AfI5Z4elVfvI8m1X9jL9nrWIj9s+FOj5IwBCGjb9CK4bxH/wTL+Besq0ml2+p6az4OLPUdwX8HBr6YjRCAMA0/A27cZ471588jyet0OSeXUH9k+KvEP8AwSvsjJ/xS3xDnhUDAS+0xZc/8CR1/lXn3jD/AIJq/HrSQ/8AwjY07VY1xgwXRhc+2yUf1r9FAqHgUpiRhgDPvXn1eEcrqbI53k+Hn0sfkt4z/Zf+PfgFGuvEfwz1i3SPrOlqJox9Sma4J4JrZmhuYmV+QwYEH06HpX7RSafbXUfktGpBGORxXm/xF/ZV+DHxJVj4s+HtjM5P+uW22yZ9QyEGvBxvBdLeicdbJLfAfkpcIyDY/GegNQkgHaelfoB8Qf8AglZ8NtaZ5/BXiPVNJbHyxyTLcJ+Tcj868B+K/wDwTe+PfgKOS88N2lvr1rGCX+xMY58eytkE/SvlcXwvmGH1S0PIxGUVoangEcm47Ac/jVm0xk59OKq6poms+GL6TTNY024tJ4mIlhuwwcH3DAfpRZXm5irsc9/Wvnq+FxWHfvHi1aFam9TVgYiPDHvUiruNVYpgF+8MZqZJwUJPBxwa41q7kwutyGRidxDAdqhUZPSlmY7etQiXPGapSaZon1Ppb/gmn8VD4M+Ng8H3khNvr1qYRluFnQGSM/UjcPoK/R6B98asOQQOR3r8bPhz4vuvA/i+x8aWUpWTTLuC6TaevlMCw/FCwr9fPh14ktfFfhOw1y0lDxXsEcsJz1V1DAn8M1+v8F45yw/spH3eTV+fDchtXSMIT82flxxX4Rf8FOdO8W2n7Z3jz/hL7ySZn1VJ7F34AtHhVYo15+6pD/iTX7xP8yYwMkfrX5V/8F5/g8dE8Z+F/jFplviPVLefS9QYD/lon7yM9OpBcfhX2mNj+7bPL4qw0pYBn52xD90EqW3QhvlNRopxgCrNlt8wnI+U8185Qj+9PxvDtwxB++/7Bs9jd/sseAJrBg0beFrPbg8fcGf1zXss8sNtEZGYKB3PAr8bP2SP+CtnxQ/Z0+FVh8LLvwdpWsWelQtDYT3V5LFNDCWDIrbFYPgswyMcYqz8Wv8AgsR+0x8SYZdM8OahY+HLeXILaTEfNA9PNlDN+KqD719BTxlOnSsfrWA4iweGwCjJ+8foH+17+3N8Ov2ZvCl19uvv7S1koUsdFgmCzTM3Q56CP1c9M8V+PXxU+KPiT4yfETU/iR4wmE2oapObq5ZGzHGDhY4V56KOMe2e9ZHizxv4h8a6i2teJtbur66lbMtzcTPNI5z/ABMxz/SqNudr5PXPFcFfF+00Pkc7z2pjHyL4S1aQqsZYD6/lT0QAEmi1ZdjR57cVF9o8vOTXnnyL3GOOSKjYBuopTOM8kZqIuucj1qb30ENWKRpMxgkdRgZzX7Yf8E5vhBJ8Hv2ZPC3h+6s/Kur6z+3agpHSaf8AeMP++dqj8a/Jj9kv4P3/AMavjt4T8C2cDPb3uvQC5287LdP3srH6Kh/Ov3a0Gxh0rT4rWCMLHGgURjoBjGB+Ar08ug1LmP07gzAP3qpfS4wA0gxXzd/wUp+L4+H/AOz9daBYXfl3/iG6GnREHDCLO+VvptwPbNfQ95ME3Y7Dp+FfnH/wU4+JT+MvjtH4JtZy1t4esFjdQ3y+fL87n8FAFcPEWN+r4OaPt8yrqjhpHzTBEZMkrg5JHtU9qhTg/rUkVu4UEDt1pQGU48uvwetJ1KrbPzycuaVxxY457008nJP40m891/M0GRf8Kz0M3YVZWAGM+1NaciQhexOOaiaQjODz2xUcaz3JVIoiSxA4Gcmpo4bF4iVoFU6FarL3Sx9oAXcSOTwaek+WAz+Neq/CP9h/4/8AxamiurLwxJp9jIObzVmMMQHHIXl247gV9G/DX/gk74asGS9+JPje61AjlrPTYRCp9t7ZYj3AFfVZfwxmGIS5onrYbKsRU3PiRI5ZPuofm6cVs+GvhJ8SPF06QeHPBWo3jSdDb2sj5z39MfjX6c+A/wBkT4G/D+KMeH/hppHmJj/SL2P7RLkdyXzg/hXpNhotpYRLb2ltDEijC+TGFA/75r67B8EW1mezRyOmvjPzT8G/8E8f2h/EhVr7w8mlxN31K7AYf8AjBNeo+Gv+CU+p3MO3xX8RY4jjlbDS2bt/ekf+lfcUcQVmB7HHWnlUYE4yOxr6PD8IYKmtT0aeT4WB8j6L/wAEofhhAg/tjxdrlz0yqywwg/8AfKk12fh7/gnD+zrokSQz+DWvTHjL3mpyuWx6gECvoVR8oNMiYAuD0J4r0qXDmX09onTHAYWB554V/Zh+C/g4xnw98MdCgdCNr/YVZuPd8mu9s9Et7fFvDarEiAhQoGAMAcY4qWBQUdfXgZqaGEqMp29DXpUcuwtLWMTWnRowfuiIhiURYwUxmnAg9KsAbFwe1MruiklZHUFFFFUAUnlp6mlpE+6KAFooooAKKKKACnK5JwRTaASDkUAP+X+7+lBYDrQDxk0m75vagBw6dMUU3zPalDBuooFqIygL9KbzmpKKAWxHS9+v40+mlPQ0DG0YA6ClIIPPFMPHP/stADg27mgDsKbHnHNOwcZoAAT0BoooycYzQAKT5WKIG/c4pIh8zk/hS0AODKP4aXevrSL8q7qb06GgWgUUoBPSggg4oGJjyjgdqbHJng5pwJHSo4O9AEgJByKcuAu6m05X7E0AIJcn7pqNiCeKlG1uAKZ5a+tACSn91j2FQeXmPI5PpVmoYuBk+9AAT7c0gBPSkJ9TUydelYXZoNxz0pyfd4pVxt4pLfGyX1rczIaLfgHB70117j8aW2/i+tAEoIPSkUYHNIQOCfSpl6D6UGYUUUVzmj0DIPQ09fu8VEoO7JFPQHbn2roMlsG44xQpAPNCfJ3J9qfgHqKCoBTfM9qF+7z0puTnOaCxytjhqXJ9VpoJHQ0duv4UAJSxY+bPrUeT6mpACTxQA+imoecU6gV0FFFFAwqPnNSU1lJb60AJk+ppKUggZpKAGoO9JGm3k0+igBIosg5HGO9EaGE8U5c54NHzfdoAanT8aWkTp+NLWMgGwDbI5pQcjNNH3pCBTkzjmtIXSAWo2/1Tc1JSbB6mqAZT06fjTKkoAKKSE/uce9LQAUUUUAPHQ7arRkp1qak2qe1BmQWvLScD2qcFQMbv1qrYIfN4FWPJlB3Fhip+0aD6b5ntQd3le+KiY5Oc1QCH2prKCD8vT2p1PjKhWcnoc8/Sk9hrc5Xx940i8E+Dr3xVdktHY2ckzpnGcE4H6V8ey/8ABRP4tT6lNLa6Lowg3sY4nEgYLnjLA8mvqH9pHSjqvwX8S6fDwz6NIVX3A3V+b1sgClxyCOD+FfzP4wcX5vw5Vi8NLc+44VyjCZin7VH07ov/AAUk8XRhU1jwNaNtIDtDqJH/AKEhBrstD/4KO+DLiLfrfhzU7cEcmERTAf8AfLA/pXx1bowGF/SpI7SORiSoGDnGK/GMF428RYZ2qO59fV4NwFRe6fevhr9tb4H+JAkf/CWiyZiMLfwyQkE+pOR+temaD4/8L+I7JJ9D8R286sBhoLhJBj8K/MfycQbY5Soxjg9KtaTrmuaIyyaVq09q+eGglKke/Br7/JPHytJf7UjwsZwK1/DZ+o0N5BMR5cqHPoaewUnGOfXFfnr4V/at+N3g9Ujg8WC9iQAeVeKWOPqK9V8G/wDBReWB47Txp4NmjAXDz2FwJAPfY4B/I1+o5H4yZBj5ctSokfNYvhPMaC92Nz6025OzFD2MUiYkQEe4rzL4e/tW/Cr4gzLa6T4rt1uGz/ot0PKlH4N1/A16fY6pZ6jAGgkB45AHIr9HwPEOSZvH93NP5o+br5XisPL97E4T4m/s4fCz4rWj2vjTwPpd80g4luIB5i+4ZcEfnXyX8dP+CVD2rza/8E9X2mMMzaRfSblc448uTqOegPFfeEqFRhWOPeozArjDAHjvWmMybL8XStGN7nlVsHRqq0on41+N/hx4++GGpto/jjwreabcq21Teq4Df7jD5HrDW5GCmefTvX7D+N/hJ4S+IWkS6L4o0C3vLaVSrW93ErqO2R3H1HSvkD9oD/glZeh5fEPwS19YlB3/ANi3g3RsP7qSdV59a+BzPg2dP3qOx8/isj+1A+M5J1PAbP41A8inhWzz1Fb/AI9+FHxB+HupyaF408M3VhdR5/cSRkBvQqx4cH2rmASo2Ecj73HSvicXgMThJWlE+frYWrQlqXYLgIMA/nX6W/8ABM74oJ44/Z7stEuLjfdeH7iXTptx52A74j+KHFfmMbgKucZFfUv/AASm+Kkvh/4v6n4AnuWFvrmmefCmePPt25P1aNz+C17/AAnj3Sxqgz2shxSjWsz9JUAZQucjpXyP/wAFjPhjJ4//AGPtYv7W2Lz+H7u31KIgZOFJV/8Ax1v0NfWdlOrxKccYHNcl8cvBll8Q/hjrfgjUIQ8WpaRPbSBxnO+NlH/oQ/I1+2NfWMOfRZrTWKwMkfzoMfLZgCDg1LaDzYt5OGHXFWfFWgy+GPEmpeHrsbZrG+mt3RhgqY5Nh/PBNQWUG5N1fO1KbozsfhmKovD15Ims4igbB6nirtpkP17VFBA4Xhs1IqEcA1i+aWiIp3m+UvwOQMg8dKswRNIRsGT2wK9v/ZE/4J7/ABr/AGoWTVdMsH0rRd+JdZ1JSIn56RoPmk475xX3b8Jv+CNX7PXg+KG78ctqPiO6RRvF3dGGBj6CNOSPqa7sPg6kldn0+X8OVsXT5j8qHjmhxuyPxHNV3mZT8xP5V+2z/wDBPr9kx9M/s4/AvQlTbt5tvmx/vA5r8zP+Clf7MvgT9nX46Q6P8PIpLewvNKS6jsml3LBJ5u0gd8EDgH0rWtgnGHNcyzXhuWX0XVb2PnyN1O8HHtUKSksR7/lRGTgqe9Mt1MrlVGcnAxXlQV5HyWHftKqR99f8EQvhhHrXj7WvifdWxI0exFraPjgTXDZb8o4//Hq/TtY2UD2r4/8A+CMvgKHw3+yzH4kaPbNrmt3VwWI+8kZECf8AoB/OvsbHGwjHHUV9FgoKNI/dOGMP7DAI5L4leL7DwR4T1HxNqswWDT7aWaZif4UGf/rV+SHjXxne/ELx3q3jPVWJudTu2uHyc/6x87fpsCj25r9Av+CmHjs+EvgBeaZbS7JdcvorMYb5trHc/wCG1f51+cEJbzAwYjnj/CvznjHHcr9kcWf4vl9w04wMBQKY5G85wQKha5KoSv8A+upNN07V9fu4rLSrS4nuJnCRR20RZmJOAAo5NfnGFwmIxFW0T5ejRniHZFWa4VMlQOO56GrGiaDrWvXcdhpdlcT3E7AJBDCZHYk8AKATX1N+z3/wTA8XeLPsniH4yX0ulWcqh20yDBunGRw7dEBHcc19j/DD9nT4VfB60W28FeC7KzEabTcxx+ZO44+9I3zN68V9tlXBtesuaroj6HB5HUkuaZ8Q/Bv/AIJr/FHx9BBf+N5B4etJFBC3EXnXJX/rmCFX8T+FfVfwV/YS+Cfweli1O28NrqeoW6fLqOqOJZQeOVUAIv4DPvXtkVskMYjRQFA6CpEYdQ3HrX32A4WweESdtT6PDZbhaMfMitdLt7RQscKgAYGB0/wqcDtj6UT3McaHL7cDrXJ+MvjB4F8D2zS+JvFtjbMF+482+Q/RAa+qo4SnTVoouWKw+GWp1EbI3mg8+opRNDCOWCj0PFfNHjf9vDSbSaS18E6FLeYyFub2QxqfcInJH415X4n/AGvfjd4im2WHiQadCfvxWlvGhx6b23N+VdipHi4vijC0Xofbep69o+j273Op6rFFHySZ5VVR+fNcVrH7Svwj0BjDceM7VigPyQRPLXxXqHxA8S67OZtZ1yadj1a6neQ/rx+lUp9QkmOTLn3pezseDX4tVrwR9W+I/wBufwLprNFomk6lqGDwyokC/rk1ymq/t9X7xkaX4Fgj44N1qTH89q185yTuzYY9OhpmTtdjijlZ5cuKsVNntc37fXxBW6ydF0eOMN92OSV2x+Ir379nT9oPT/jfoL6nFbGG5tX8u5hP8LYr4KeNJD0HPtX1T/wT40FbTw3rWt7cC51FEGR12Kuf51nKNj2MgzuvjMZySPpuNfNi69qWi027Mq3GOtOZWJzkVC2P0HdCOMNSUrfeNJTNRvl+9OopkbtIeBQA+iijBPQUAAJByKKKKACiiigABI6UUvzfepKAClXqPrQn+qoX73WgBwz3FLQAAMCigAooooAMA9RTWAC8LTqKAIkPy09cBd1OwPQUAADAoAbyi+9AUty1OooAQqD1pNno1OooAAAOlN2/NinEgdaauS26gA+ZKAyn7wo8z2pqDbgUAMTmMj3NEWI+h7UlR0AWKKjg71Kn3hQAoZiOFptLFJzgnNJQAU3IJbFOpGBI4oAgUKCP3JqQEHoajc4yaZCw8xwMVyx3HqiTcc7qLb/WtzTEGfmzRbN8rE+p610rYQ8g5P8AjTYOjn360jAEbhS233ST3NMCUAgDNSVHTywAyTSsjMexXGRim0yM4jzmiMZGR69c1gaE0ajfg0EAjFLDmiughbIbF9+lGAMA01d38NEf3jQENhKUDJxmkIIODRQWHWlBIGKQgg8iigBqdfwp6ru7005A+UUils85oAei5OafTYwNgNOoFbW4UUUUDCiim+Z7UAEnam05Vz8xppBBwaACj7o+lFFYyAfD+635FInX8KjaUdP5mnw8wj5u9ap3APK2jgmkqRuh+lV6HoiFuSx4yfWkpEBx0pxUgufalTNHuJRRRVCCkiHzPTDNx1pN6+tACQg8detTVH1p8cnPSgBaKKKAChuh+lFBGRg0AQW3XpUkeDCNopVUg802MfugB60nsRDYKj+lSQkAzio6ZYjnC1A245AP605+v4UifeFLRoDnvG9jFqmg39iz71ngeMBh2ZMYP6V+Y99aSaV4iudKnXa9vcSxMhXGCshXFfqVqVmJ4pFUg5HWvz0/at8IDwP8c9VtxBshvJEvbcBSMrKMN+TKfzr+aPHbJ3iMtddL4T7ng3FezxHJ3OEsm+Q7uoqW2c+a4JqtDIQpAPU81LbOC7DI5r+LGnzH7HBr2ZKGJBwacriPknr39ahTkkDrnj3p0TSZJEZbHXiuvCYPE4ufJRjcyqV6dFXmywrFlyDmo5o1I+ZeKuWGk61exh7TTZ3BGf3cTNTbqO/s5TBewzwnv50BX+Yr1pcO51hI+15H+JwvMMBUly8yM94HRd8bEbeQR296774W/tN/GX4XulrpOvz3Vkmf9F1KTz41GO3O9f1rjShYZHpTI4EbcxHI6V05VxfnmRVn7ObXldk4jK8DjqfvRufYnww/b78Ja4iWfjvTZdJuVGDcRMZYDx1PcZxXvPhTxvoHjTTk1PQtXgu4nHDxMMDj2r8yoIh5Q5x7jtXSeA/il4/+Gk4uPBuuzWhzl0aQSRP7lPxr914N8b69J8mPPis14KpzXNh2fpWiqVCn8M96dNBE6bXAwR3FfL3wW/b003UFi034qQLp8q4U6hCxe3Puw+8hPPqK+kfDnjPw94n0+PUdG1KG5hkUMksUocEHpyDX9JZBxnk+fUFONRan57j8oxeBm4zicz8Svgv4P+KOlzaN4r8OWt7bSAjZcJ86k8b42HKHHSvh/wDaa/4JoeNvCZn8T/CBX1SxT5msSB9piGPujtJ9evFfoyJFfv26VVliilLROgbB5zXs47J8DmND93ufOYjA06itNH4beIbDW/D11LpGt6fLbXEWVnhliKuuDjDA9O9dH+zt8TW+F/xj8OeN1chLDV4vtIHeGT91J+jV+mX7Tn7FXwz/AGgbGR9Q0j7HqkRxDq1sipIDj0/jH1r4a+JP/BNr48fD/wAQx2/h7TBrFhJMFjvLPgjJGC69Rj17V8GuGq+AxntYI+deWVsLiVKGx+pXhLUYtT0yC6hYFZIwykdMYBH86vX0azIdwyQMfWue+Fej3nhzwRpejaid09nptvFO2c5cKAe/tXTSgGPgda/ScBzrDJSPq3Dnw1j8Dv8Ago/8N4vhd+2b478PWkapBJrTXcCquAEuI1lH65H4GvGtNkBTb+tfaH/BczwB/Yf7VVl4xt7bEeveGIHdguMyQSPEfx2sv4V8W2EWw47DivNx0OWqfh/EMVSzCUTUtRvAC19J/wDBOP8AY1k/aj+Mav4gtZP+EZ0M/a9dlwcSqWHlw/Vtp6fwg5r5y0eAT3IRMkMcYXtxX7Xf8EyvgJ/woj9m/SLC+0/ytV16Iarqcm3lXkx5cf0VAPxJpYShz1Ndj0eFcrhjMS5VNke8eEPCGh+ENFtvDvh3SobSztIliSGFQqxqowFAHpxW4YBtxt4x6U2FAGyOBnOPrU0eAmTz1619BFJaH7Hh8PClDlitDLv2SEMCeOf5V+QH/BX/AMYwa3+1tq+k28wddH0iwtXCn7jnfIw/8fX86/WH4k+MNI8E6HqfibWbpIrTTrUz3Ts3CoiFmP6Cvwa/aA+JV98ZPjJr/wATLrOdY1ia5X5slYmICL9Nqr9Oa4sdNRp27nwnGGLpxoOl1ZyiykjLHrS2iNNMqw5GRkAd6gPysF+ld1+zR4BuviZ8bPC3gaOPd/aOvWFsQefle4LOfwjVq+doK9Sx+Y5XhnWxkYruftN+w58PP+FX/szeBfBTWxSS18P27XAx92SQGV//AB5q9ikYrFxjJ6GqXh2wTTrGO1ijCpHCFVR0AAAA/ICp7mbCEKp/AV9LyONA/fcFS+r4TlR8D/8ABWTxpcTeLPDng6Kf93BbXN5LHn+IlYl/TdXx+OV+Xpj7w7V9qfts/svfGL41/Gmz1nw9oRmsX05LWOdW+SMrIWbf/dzkflXX/s2f8E1fCXgm/TxT8T7qPWrtcGCw2Yt4Dx1/56f/AFq/PMyyXEZnjb20PBxOAnjcRdny3+zz+x38XfjxeRzadok+n6UHAm1nUSyxHp91DzIMfhX37+zz+yH8NvgJYxTaToq3mqbQs+sXUY354yEH8K16fo+i6folgljp1oiQwgIiIgAQAYwAOlXRMGyueO9fTZRwvQwceeW57GEyvD0I36j0VYk2qOAOKA3y7gevPFUNZ1y00ixa7vbuOCNOXmlOFUD1zXi/xF/bY8C+FDNZeGmbWr1Dt2wtthXty/cfSvq6VBQViq+a4bB6SZ7Xf6paaZA011cIiKCSXPFeP/En9sPwf4JuZdM0cSardpkGOHCxofdvSvnrx9+0X48+I8pfVb9ILUj/AI9LN2QR9OOfv1wlxetcLlmB9K2jFxPjcy4njG6one/FD9rP4v8Ajt3tLfXF0uxbj7Lpv38ehc+3pXmFxqt9du0t3IzuRy8k29z+Jp7gMrDFVjEF+71rWMkj4/E5rjMU/iBJywznmniUnkfzpq2Us4EccZYnsATmrMXhnxI8YZNJusHoRZP/AIU3I444TGYhEAmBxz9TUsc+QMNxUc9je2TeXc27I2PushVvyNRxO4GWGCam6Zm6FXD6SRcUqUL9/rTXlyuA3FQCZsOpPfimGbcMY5o0SH0J4I/NkCj1r7a/Y60AaL8FNMmaPabsSzuSOu9+P0H6V8W+H7W51a6FjZRF5JzGkQHd3wg/Wv0U+HHh5PCvg3S/Dqx7Ra2aR4/3U/xJqJ2PueEMD78qp0FkSOtKD++kFNs/3sRIB46ZqVc45FZLY/S6fwgn3aUnHJopH+6aHsWNhOQfrTbY7QfmpYjhTUQBaLHvxWNLqQ9y1ERIpziliHyk+9VckdDUkMwxjH41uIlI/e5A9KQjHBojOTJg5OOlK/Ye1BdNiUUUEknJoGFKFONwNJT1BAwRQAm35felXGOKRPu80qdPxpUwFpMAHgUtFMAooooAKKKKACiiigAooooAKKKb8yUAOpsfej7nvmjeOwoAb0opxBX7ozTaACNDu3E0UkZ4yDS0AFNEoU4J/WnVDLGOpoAEPapo8cfLUAU+h/Kp4uUIoAfjp7UwjsRSq3yg+9DdT9aBLYpMcEmkgwZHYdzUzrycDio4lwzE9c1yWszbnQ6FBndnvRb/ACrJj14pyL6HmltlI3HHrXTDVGTaQ2hNu/3oyT1pYgGlODxVAPpFcrnn1pE6/hTXBGTigzEjJXNOilwcEfpUaZIyR+lPsSPMI9654Ghbjzk7aFzt5pqtg+1CjkV0ER3FjOG60BlU8ClwuM8UiAg9KCxckj5Rmkwc9O9Kn3RS0ABAPUVEFA6CpaTYvpWYDKVBz0pViGMkn86UADpWgC0UgAHSloAKKKa3y/doAbQTk5oooAcmaN3ze1HzbcbaaevXNAACR0NI373n86WigBvljGM/pRHGIvumnUUAJDne5py9R9aSlXOeKAAsSetJSpkwBjSUGYUUVHQaD3iiA+7+NRjGcbfpxUsfVvpQAB0FAobkXk8ZOfzpYu1SVHQMkooikwOhooAKKKKACq9swjaTPY8VYbofpVVDidj70rom+pJ55PmQ460uwepqKAEtJuFTUJ3KKrg9aaRjg1b8keWAT3qJrcnmmBShGCd54J7j3r5O/wCCingcyXGjeObSDHliSzuMn7oJ3pn9a+uAg69Oa8u/ah+Hc3xE+FGq6Lbj/SPsXnWrY6SxkkfiRx+FfnXiDk6zbIqsH1TPUyTFvC4yLPz1yI1wDx/OnRBQPOVelNmtpIG8q4yHBK4PYjAx9c0yKXYpVj2Oa/zxzHL6mDzGdCW6Z+94OvGthVURqaHp194h1G30nS7WSS6upRHCiLncTjA/z0xX2B+z7+xZomgaZb+IfiJbpqF+6hhasN0UOcEL/tV5n/wT/wDANl4l8YXXjO+hDjS1SK2LD7sr8k89cLX3HZRRQW6pGoAxxjvX9U+EHAmX4jBrEYiOp+X8V55iFXdKm7HOab4I8PaXGtrZ2UMESgBUigVQB+Vcb8ZPC3gSXw/d32u6TZyQW8LPNJNEuNgXJOQPavS9QktbZJJ52Gwdz2P9K+Pf20vjzDrizfCzwpd/uywXUZ4myNoJ/dg+h71+j8dy4byHKJxlCPNbTY+eySGOxuLTvofPiXVte3M0lnHshZpHhQ9VXf8AKP8AvmmR5CkZ+pqK2HlqFXgYwD6D0qdNuOP071/B2ayWLzCpOnHRs/bsJ+6w0YyY5dwiyGpHmcDr+VMkIOTnpSEKy7s9sg56157wuIir2Or2tLa5WkLHfkkbs9O1avgL4wfEr4T3/wDafgrxHPCgYFrRZtyP65jPB69qoS4kjwD261U+z56DNe3k3EubZLV5qNRryOPE4HC4yFpxufYnwK/4KC+FfFc8OgfESz/sa8YbftQJa3dvTJ5Qn3r6P0jWbTWIvtOn3KSKw3bkYNkeuRxivynW1XeWx0zXqHwF/aq+IXwa1RLK9uP7S0Xd82nSzENEueWjfPXH8Jr+kvD/AMZJOoqOOdj89zzg12dTD/cfofOm8EE9uM1XNmHIl8vnv6muP+Enx48CfGLSY9W8L62GMYH2mzYhZID/AHXU89utdwGycjv0Ga/prKs2y3OKKq0ZXufnNfBVMPUcaisLABHH5aLwB+VSNym0dcdabbhtj565pWxs4/CvatFKyMrK1j85v+C7PgcX3hnwX46EYLWmp3unyvtz8skSyrz/AL0Zr8zhCqPgDHPUV+wH/BYvwl/b/wCyvcaqI950nXbe6BK5wDmMn8jX5D3kAWYhOzc4rw8x/iH41xbh1HHcyOy/Z+8OW/if4p+G/D1ymUutZs4H77g86An8sj8K/oG0Czhs7GOzt1wkSBUUDoBxj9BX89Hw08Wy+AfFen+MoVDyaXf213EpP3jHIr4/HGK/X3wB/wAFZP2N/EvhW11nVvi3a6LcyRoZ9Pv7acTQuRkqQikNz3BxWmCqU2rnscI47C4anL2jtc+q4wFTLdqq32rWmm2ryzXG1FBZmPYdc/Tivlnxx/wV0/ZC8NW7nRvHN3rkwjOyPStLkIJ6YLSBfzr4u/au/wCCpvxW+OUF54b8Cxjw74fclDHbXJa9nQ/33AAAIP3VrsliqSPrMfxHg6FK8ZI77/gqh+3xZeK47r9nr4XaxHcWwlC+INVtZtyyBTxbR7fvDn5m9eO1fBOxpBuIxkcLU8rS3b+a7Ek9c+9O8hhHyPpXj4uv7eR+QZzmk8yrORQeHa5I65r6c/4JK+ED4w/bG8MXnl5i0lbq/kH93y4GjU/QtJ+dfNc2FbAPTvX2/wD8EKvDFxe/HHxP4iMRZLDw4E3k9GmuOB9MRmscJTvVOzhigquYw8j9V7VfkC4yAlNnyQFaPH4VLbDBOeuKW4GV4r6iKXs7M/c6C/d2M0WyNOSE5PepYUEeQBz7VKhUMynoDWT4o8XaN4S0qfVtc1GCC1gUtJLO+wKB/OlSoRbukc9adLCrmmackiRoXY44yTXlXxj/AGmvCPwsjezmeK/1HB8uztpRxxwXPYV498aP23dQ8RLJ4d+Gk72VvyjanNHiaTBwdifwoc8MeteBXct3qNxLdXdy0krHdKzvuLH1z3NdsaXLufIZnxJCF40jrPiz+0B8RPi3dSnX9SaG1QE2+n2jFYVXsCerGuKgUmIMPy9DTlUgc/UU6M7ThaZ8DicZXxdRznIFkKY+aniWEpkMOlQXOBGVB5qo0zIOeOO5qHfqcMlJlqOUuW56ims5BPSq6Tkcgde9PEuQCG/GkkwppqaufUH7C3gnwX4g0O713UtJin1S0vAkhnwyiNuVZQelfUEfhvTvJEf2KHbjG3yxj6V+fv7Ovxx1T4N+K11NmM2n3KiO/tM8hMj94vqeenavvnwR450HxzoFvrmi36Twzxhg0bdMj+dTNNPQ/UuHp5fiKHI7XRynxT/Zv8A/EnS5YNQ0aOK5Yfu7qFQro3Y8V8T/ABr+DHiP4OeKTo+roz28oJsr3b8s6g/+h461+kAdJFC5zx1NeU/tTfDKw+Ivwq1ew8gfa7S0e5sphjcroM9fcAiqgbZ5kuHq4fnprU+AEbjhs575pU+8Kc0flgRsmCAOKZao2C31wKaVz8v+rtVuQ9c/Y88Dr4q+KljdTx7rfTWa9lOP7nCD6Fj+lfdVvD5UYX0H5V84fsB+DEtfDmpeLZ4SpvJ0t4GI/wCWacn8Cc19KqpKgAYwaiZ+s8NYVUMKmMTPkuAO9Mhj7k8fWlZQfNx2NEQxGfrWcT6YeHGOc0IO9Np6fdFUA7aQOlQJ0H+8akjwsI9e1OU4X8Kx+0ZlWEgB+e9Lkbevai2G4uMd6kWAZ+VTWq2Jp3JLdmRMH+dLRRTNgooooAKGyFzQPvD60ZIZyPSgBVI8qkBIORTNzetPiPyGgB4YE4FKBgYqMdeuKevTpigBaKKKACigEEZFFABRR1ooFdBzn2o6UU1X/vGgYff9sUrFTxmlpnfr+NADt49DTOnQ04L3AzTqAI6KUg5xSUAEfyVHHKPnGPWpKVRk0AJR5J96kwPQUmOmO1ADEAXPPalTgk0JHnJzR0INBnAeenTNIwyMYoAHp+lLgYxig0I9u7jFRSRhBnNTRIsfRv1pOlcnUBrKoGcUWv3P+A0r/dNJGRtJB7V1UzJ7EK9B9KWzA3En3qNmOcCpLfr+NM1EBIbNBmHY0KeRTx/q3x+FTIzIxICOTSwAelMDseh/SprIbTkj86ygaxdyyAAMCiiitzPlYJ8o6frRRRQUthIxgtxS03u3HakBOciH9aBj6KAAOBRQAUUUUAFFFFABRRQTgZoAAABgUUzJ9vyo3fNuxQA5mxwKZTvM9qbQAUUUUAFFFFACrjOCM0+owccilHOBQAJH5ZApKkqOgIBQD3BopIT8747UAEYJGBS0+MEbsDtTKVPUzCo6koteDk+lM0CiiigCJn7RHOaLYnOcVIIhFz602PbzQAoGZJCOwqseZpPrViAHzJM556UxwyDIH6UEQuR20o+fHepU+6KgjX9+MVYA7AUrIsKKKKYFaRJPT8ao6pb+ZbmMqDxgFugrUKkDkVVvANhUdjxXn43CfW8I6cgpt06nMj85/wBrPwEfh18YNR02C22Wt24vLIKmAFf7wB+teaK7OjDPXvX2X+3/APC1/EHgJPHdjAXudFwXwuSYHHzDj0OT9K+MrR1Y5U57rxwfSv4P8VeH6mU55KvGOjP2jhfMFicEqcmez/s4/tO3nwWsRoVz4dF1ameSYPDcBJQzlc5B4bpx6V7en/BRTwYkG2Tw5qqyAD5fJiP67q+N4lY/OxyB0BOcfSrNvGHXoMjviuDI/FPO8mwioUtloa43hXBYys6kj3/4qftu+MfHEE2jeD7FdMtpVKyXM8u+cg9QoHyr9eSK8OmkuLuctdTM8hYs7OxJY/X1qNAoAZeMDscUqLNcSeVFEzuxAQKMls9PzNeZmHE2e8Y4tUqkm7nVhcqwOUUnJdC/pPh291+4istKtXkmmkVEjii3szHoAOvbrXuHw8/YE8aeI401Pxfqv9jpIMrbhRNKM44OcKK9R/ZG/Zng+G2lW/i3xTbCXW7yLzF8wA/Y0bB8tff1Ne+BNkeD0A4A7Cv6F8P/AAewksFHE41Xkz4DPeKsQ8Q4Yd2SPmmL/gnf4Pt0LTeNtXkI6j7NbDP/AI5Xkv7T37OOl/BPTLHWdH1OaeG7n8iaC6VVkRsZ3gpwfTFfdjFnO0fhXyt/wUl1fyNM8O6LE+Gn1GSR1UnO1U617HHvBWRZVkVSrTprRdkcmR5xjsVjoxlJs+Wrdi0ePakAGCTRbAiPA6U9FDREj14r+IsRFKu0j9notumrkIQKu4dxVV1zuHHvkVeZfl4HNVZELNIvXiohOdN3Who7PRi+F/F3ifwLrKeIfCGvXNhdwNlJ4nGcj1H8YOeh9K+yP2UP219O+J9yvg3x9cw2OuomIz92G+XP30z9yQnqh/Cvi5oWIx6d6igtJ4LpdQs7loZ43EkbI/3WHRhznNfqvAviRmmQY2MJy5qfY+Xzrh3C46k5JWkfrRaXMc0e6FtwIySD1p3fgfhXgP7D3xs1T4jeDJNH8RXjTXulgJvdvmZO2ffivf1wVDfrX908MZ7Tz/L44im9z8Zx+Dnl+JdKR8/f8FGvDy+Iv2O/HthFHl49Clmi4z80WHyP1r8Pnl8yUk9+a/oD/aJ0CPxV8IPEfh2WL5bzQruHaf4t0Lc1+At9pkljfyWrD5o/lYfQ7a68xg27n5DxnR5anMQ2wZ1KMeh4qxawdTkjA456UtpbKyFlNWbS1YFyRXk05OB+eQrVY7MdYxsyEFicHjJq3DETGc0lpa7U4OOaspDkENwfaiU2wlUrT3KqwqDuWhwQuQasNDgdajki/dZJxz3rN67BDzKEyBnKkd6/Sb/gg3oCweGPH+vbSXbUrC1DH0WGRyPzYV+bcoZGOe/Wv1K/4IXaWbf4D+KtTIOZ/FoUEnrstY//AIqu/Lb+1ufacG0efGufY+64uEx7Uk7YGzPPUe9NQsGyWrmPix4+svhx4H1LxjqSEx2NuWKjqzHGFHtyK+igueR+tVayw+G52Y/xm+NXhv4QaJLrOt3mXIKwWkZG+V+gA9s96+JvjD8ffGXxf1WW7126FvbRsTa6bEx8pF7YPRm9c1S+KfxK8R/E7X7nxD4luzuYsIEBysSnogH41yscBXAAx6D0rsiuRWPzXOM7r15uMdiVGOwcnj3qeIhTjFQpHgbc9Kfwo60z5OTctybIJ3HrQm1mGfXrUfmZ6n8qSOXLAA9+tBmrXPRfgD8OtG+JHxAsfDWq58uVJDKVODnZnH4V73ff8E+/hbcKJLa+1GI4GfKnBP65rxH9kDVEsfjbokU0mBNLJGCT1JjP+FfeURVYgD6Disqi94/QeH8uwWLwrc431Pjv4k/sCa9okMt/4F1tr5EQkWl9ABKT7OpwfxFfPmtaHrvhbU5dJ1+xkguYSQ8ciEYOO3rX6j7BLkNGCD2IrzP42fs6eFPizplwmpafHFdoD9ivYFCyIcdz3FONW2505pwxh5UuakfnzAzQkMCeua7f4Y/H/wCIPwouQ3hLUw1sTma2mO+Jj346jNZfxD+HOsfDzxNdeGtZhIltDl5AMCRM4DiuciU5LYx9KrfU+BVTE5TiHFH1N4a/4KLCOxEeu+BpPOVcH7JqC7WP0df60/XP2/NO1jSLm1g8B3cTTQOiNdXyMPmXGcIOetfLcS7gW7ipYiQu38vajmPVfEeMnDlZLqE8dzK0yLjdkgfrUGmwyXk8NpC37x2A/EnAz+dK3zgg9hXpf7JvwguviZ8SYb64tidP0iVbm+c9GbPyR/j1oirI5Muw9TG4u59g/s9eDYvA3w60rQsFWFpvlB/vtzXdjaU49KhsoIbUJGI8bOBx09qfECDyG9656j1P17BUXh8PGIRRkxuW6npTIgVbBqfaMbaYYPRqo7wp+RxzTPKOPu/rUcqEH8PWgCePheDSEZjx7UQk7257U4EHpQZrcgIyTU1pk8CmCLk5FG0jov6VMdjQkopEGFpaoAqEHEmT61NkjoaiaW4HT+VADIX39/xqSNtyyAnJ+tV2U4wR1qWzjEQwO9TIBUODg0+0z+8zSwxhhlutLCAGcAUobAOUEnIpy9OmKbGf3VKh7E/SrAdQQDwaKCcDNADeEb2o8v3pCcnNJQA77vG/9KTJ9TSUUAAJHQ0Hr1zRRQAUo4bmkBIORSgZODQA8AAYFFFFABRRRQAUUUUAFN/i29qdTM4OQaAJEz5b0xQQ3K0KG7NSgAHNACgjoDRRUa5ABoAKKKCccmsWwIw2I3+bsait2OHQHOKllA24PpUMC/6zA70UwEi/pUsbFW4ptqFUsO9PgIDPz3rYATO2mFiCwFLESSakGecelJO5mQxfMdpNSwcYxUJOH5NT22OPpUGhPRSBgTgUnme1aAOopA6nvS5GcZoARhkdKZUlIFUdqAFpOFFLkDimt8v3aADzPagSKeRTaIOp+lAk7klB6dM0UUDAdOmKCQBk0U1z/CKAG0UUUAFFFAODmgAIBGDRmIUolB6CmlAazABjBINEM0YGMc/ShRgYpaACiiitAF3t60cY6Uuw+opvOaACk2+Tz39c0tFABFNySD160UkQ+ZzS0AFO8z2pkZwM+9KCR0oAKXJ9TSUUAFQwjAA9DU1FABRRVZOWAI/OgBLYZ4x1q1aEAvmm7tpP1pICSznFBmOKKe1MIIODTiwwSDSAE9BQaDGkAHBqBpJnGBIP++almXOQKbBD6GlokBzviLw7p3inRrnRdSgD293E8TrJ3G0qf51+a3xT8A33wl+IOqeAtRt2H2G8K2zHI3Qsco3vxxX6kyQqqCPaPl6ZHSvlr/goP8D7vxHpsXxN8P2zNc6ShjvlQDM1ueQx9Spzz6V+H+LnCdPN8oeIpr31c+o4YzN4bFcjejPke2+ZQ5b8KuW3AYt2FZlrdADaW4x19a0LKXeSQa/hXG4aphMQ4SVmj9twtWNekmWYzgYJ5r1n9jL4cL4++MlrealGXs9FtmupEYZVmLYjBz1Gefwrye3ZN5YnFfWX/BPHw4ll4U1fxM4H+lXkUAY46IpY8/U1+peEeVwzDP1Ke0dT5nivEPC5fK3U+mbS38mJVOPlAAFWXA2EtzxTFwq/NxQzlQzzMAgPHHav75wk8Pg8Go7Kx+Hy56kyGZkihOMZAJB96+FP25PHMPi34x/2FZ3HmR6JZeTkNn965yw+uK99/ab/AGptF+Fmmy+F9Euo73X5ozst4W3C2B43SY6cHgV8SX+oXesanc6zq9wz3N05kllbOS5INfzj408ZYWWB+o0JXb3sfdcH5TVVf201oQRqIxg1IpABBH4VG4YjA9MnivVfgD+yh47+Md9DrGoTS6Zoq8PezAtJOM/dQHt/tV/NHDvCmY8RYvloxP0jH5rhcvoXmzznT9I1XWp00/SNKlu53I2JEpJ696seJPh94w8HFB4t0CWwNwhaASn7+Ov419+/DT9njwB8KrIW3hXSII5ePOup13zSHgHLds+1eaft2+CI9U+Gh122hPnaRcpMSvURuNrZ/Ov2XMfB6OA4fliKnxpHx2H4teJx6px+E+LnT72fXiomDryOv1qcrtUgUwKHOPXvX834nD1MJinTfQ/QqMlVpJntv/BPvxDPp/xkfRvNYR3thMrp2LJhgfrya+7oX3RZJ7V+e37FU72Xx90UKv8ArWuUPPYxN/hX6C2bloASB054r+4/BDGVauSqMnsj8c4xoxjj7ox/Glq954fntn5LQupJPYrj+tfgV8TdNXTfiBq+kMNrW+oXUR9sTOuP5flX9AeuwmTT5EH92vwb/absDp/x/wDFkCLhU8QXw/OU1+z45Xpn4NxrF8lzirC2QjKvVqKEY6VDpoHlKRV+JR82B0r5+LPzGLC0hwG29e1TxwFl+bnilgAAGPSpIiBFz6VRpGzIPK4ztqKeLIyKtD7jNnoeKjbDJk9qAMq6iOSAOtfrP/wRU0YWP7JUmpsTm+8V3sozjoixRj/0E1+TzZMn49K/YH/gkLZi1/Yq8NygEeffahIQfe6cf0r0Mv6n3PBP8eR9Sh1IwF/GvEf28tUltPgbc26SEG51a2iOD1G7d/T9K9sBAzn1r5+/4KBXEbfDDT7YgYk11G5/2Y2r6Ki7SP0HOp+zwEj49ySNzc/Wo0ciTk8Z70rnJwWqMHnr0rrkz8fqVlUqWL2l6be6jOtnZQvNK7hYkUZZyegx36VZ13wzr+gv5Gu6JdWjEjC3EJXP4969Y/Yn8Ap4m8etrN5CssOiwNOA4yGdztQfzNfXmu+BdB17S2sNd0S3uY2XBhmjDZ/E/WsnOx9NgOHfr2H5z82Xl2HYy84qNJwHGCMZ4FfUnxz/AGJbG9sJdf8AhjD9nmRS0umucg4H8J/HpXyzquia1oN9LpmqWbwyQsVkSYFXU1cHznh5rkmIwK5lsa3gHxhd+D/HmleKbZyo06/t7jI7qCVf9Gr9KPCWuWXiTw/a61ZTCRLm3WVWBz8rAEV+XMRO0AHoMZ9K+of2Mf2lrLSrFPhT4x1PykVtukXkjfdyf9Ux9+1VUj2Pe4RzWnRbo1HufXUY+UGldBJGVK5yKitbyOaJWRsggYwc1YDxgDJFcn2j9OjKlUp6Hy9+3n8NUuNCg8eWUGHtpDBdFB96N+mfxr5JX5Swr9EP2jdGttd+D/iDTmTcUspWTPPI+YGvz08klSzDk1vB6H5bxVg4U8RzoZB0PNOO0nJIFQOpBK5qGSQKCXbgDk1Z8hF30RfjjluAYYIi0vmbFA/iJ6V96fsqfCuP4X/Diz065jAvrxftN87Dkuw4Ga+Xv2P/AIV3fxK+IUesXtox07R2Fxclh/rHH3E/rX3hZRw29sIlUDjjjvWPMfpHC+VyhH2syVPlGO1OKjk03I9O1KrEnBqT7tWWg2iiigoUAnoKk5zkr+lQueOPWmEkDigjn1sNt5Oc561NUdSUFhRTTzHTqACiiigByqwPpTSCDg06PvQ69x+NADc2/wDcH5VHD0GDT9i0iRGPk0AEfenAkdDShiOlRmQpzjvQBIeuRTY2PNG8dcGm4PoaAJwcjNIwyMZpsOQOR3pw69PxoAZQc55OakwMYxUdABRRQDjkUAA69cUZPTNKBk4zShQOWoAbTlLN3oUNndTgABgUAFFFFABRRRQAUUUUABzjg0zB9DT6QdcZoAXA9BQAAMCijA9BQA1mUj1ptLkH7xNGcYoARP8AVD60Y5zRkHoaK4wGTn5c1HaNiNyPWnyjIb6VFZt+6k+vrWkAEfGM1JanAaohjPNSw87sCtIAOgzk5pIyQJCKWA4bpTnbAIYVoTHYgGAdopYCd2BTOWNSQD5fqaCiegcDFA4AxRCAVNABSg4OaSigB64xxS0AYGKKAEf7pprYzxT6YUYdqAG7x6GlSb2NMwfQ06FRmgCUEHoaKKMnOMfjQAAg9Kb9z3zTunQUm8ehoAYQR1FFOZvRqbQAUUU12B4FY/aAZv8AL75zUtRxxnGSad5ajnJ/OtgHUUUUAFFFOViW+tADqjqSo6ACiiigAooooAKKXax7UhBBxQAUUoPzZNL9/wBsUANopSMHApKACk3L1zS03yl9T+dAEbnB4NOhnMQwBQR6imMuOlBmPB7inJ0xUMUhJ2mpYc7c571NNaGjYvUk7e9IcqCR/Kl+bBpvJjqgIogNmGI69TWbrWk2OtWcttd2itFMpSWOQZyCMH8DWu0YHOOtMeHzB1zXn5jl9LHYV0Z9QoVZUZXR+bf7VPwNuvgp8Up4LSA/2NqCtc6Y39wk5aL6jn8K4KxkJjbnsDmv0Q/ac+CVl8Z/AN1obER3UTCbTplA3JKByM+jcCvz51DQdW8I67deG/ENoYLu0lMc0LDHIOMj1r+JfFfgmvleNlXpR93Xofr/AAnndPEYf2U3qPhJRMnmvZv2ev2tG+Cfh2fwpf8AhGTULdrp7iGaC7CsoYcq6nPP0rxuEhhw1LyZCx529K/JOHeJ8x4axTnh93ufVY/LcNmVDkq6o+qLj/go5aGForbwBqO4DCh9Qix07nFcL47/AG5Pip4wt5dM0YwaJA4K+bCTLLt9Nx4H4V4pHtMWMDrxT15bHt6191jPF/iXFUfZqdl6njUuEcrpe/Ye91PeX1xfX0zyzTMWlmmbe0rH1PU1BMuYySPce1SA7UzWn4K8NT+NPEtj4Utgd9/eJEG9Aev6V8jgJ43ijNo06sruR6VaOHy7BOcVZI9R/ZO/Zpn+KOoR+MvFtq40a1lxHEy83Lg9P92vtrQtHstIsEstNhSKG3QRpCgwEA7Cs/4e+C9P8GeG7Lw7pkCxxWlusagDuAAT+NbcMDCUsoIIJ71/c/h7wZg8iy+MnG8mtT8XzvNauNrvXQQkGT8OtcP8cPDsHibwfqmhyxbhd6fJGQRkZ2ZH6gV2u1hKefWszxHDHLp8omIwoIyT7V9ZxLhYVslqw6Hm4CThioyR+X08clsHSTqrlCPcHH9DUKSEDKnrWv4ohgj1u+to+i6hPgj0DNisUDAA9hX+cfFNNUs8qRXc/oDK5c2BhI9S/Y1XPx98Pj0mnOf+2D1+hdlzCMc8V+e/7GqMf2gNBAGdskxOP+uLV+hVgpFsp9hX9c+Bqf8AZCPy3jJr67oQamP+Je5/2TX4UftXFT+0J4uKn/mYr04/7amv3W1gkae64wdpr8I/2qZw37QXiza3/MwXo/8AIpr9zxvwNH4Hxkr0LHDWyKF+X1q1b5EhSqdpOGQYB461csW8ybd0z29K+ejufl1tLlqA+ZjbUiwjrnHtSWcZROvNPUHBGKsqmiEsBE1V3bMJIPSpnI8rjuTVRgSMVGqGQh2EgOfxr9lP+CUAT/hiHwYiJjaL4H3P26avxrZQDn+lfsh/wSZm3/sQ+EDnIEl+Mf8Ab7NXp5bq2fe8ERSrSfofSh4Ocd6+a/8AgoddNH4T0K2U8PqspYfSI19KO2Tivmf/AIKHxlvC2gyYzt1SXJ/7ZV9DR+I+44g/3CZ8ls55bPQVHHIdu7r7U9TgsT6VFb7hJg+tdLbsficJP63Y+w/2ANFWDwNqWtlDuu9TWJSf7kadPpkmvpGA5H8q8G/YOeOT4NxbTz/alwG9jxXu8AYZQnOMGsp7H7hw7FRwCHy2sEsRWVQOM59DXgP7VP7N0XjvQp/FXh+wEeq20TOVVP8Aj5QDkcdWNfQgUFcHvUEib02lfp7VMKlmdePwNLFUnGSPytuLea0umgnQoyEqUYYORwaWzeWK68+N9pByDnGPevXf20fh7B4N+MF9e6fAsUGpQR3UKKMKGBKuo+pINeSWysBll5711bxufjOYYeeXY58h7N8Mv2v/AIo+B9Pi0aS7S/s7faqR3yksqjsHU5/OvVNK/b+sZIEXUvB7K+0bvJ1Qbc/8Cj/rXyrYoQDxjmrMSbUYg96h2O/DcR42jC17n0R49/bgt/FPhu/0Cw8FSoLqCSBpptQVthKgZwAMjmvm51DLweD0qWT+Q4qF22jNJOxw47Mq2Pd6hVnjxzTdJ0y71/VIdKsLZpbi4mEEMSDO5+i/nnn6U+WQSnanWvqL9i/9mubSUHxZ8UWmLtgf7MtJFH7pDg+Yfc9vShOxvkeXSxte72R6/wDs6/Caz+EngW00FYx9rZRLqEgH35SOR7gdPwr0EYz8vrS29sIkB24wOKkhCl3BXoawkuc/Y8Hhlh8MoRHg5GaKKKeiRuRuS4xSQ/eo/wCW340x0OcZ78UzWGxYohAIINJD95wKntMsPlPektjIr4/dmo4gRNye1TUUzQKKKKACiiigByMTwaG+X7tCHtS7x6GgBlFFFABRRRQAwBs9KeCQciiigBVbHBpVKk4202igBysM4AqKL+lPooAKKKch7UACp3Iozs4606mt/v0AHme1KGB6GmU5QoPDUAOowM5xRRQAUUUUCugpAoHSlHTpigAAYFAwpnk/7Zp5IHU0gYHoaAFAAGBUYAA61J0qIxr60AKSScmmJ94U+MeWepNRwHoaAJCQOTUb7cnNP/c+9GFPzUAIudz5qCMhVlyalJwM1VQARygUGZKGGOTTrchicetQN8zYFTWuMcetBa2JxgfKKbGcQD6GnRH5mPpSAgAiktiBintjFR2xJfn1p7FduAajQEHOKgqJaQxZ/wDrUQ/6lvxoXoPpRWhQUUUAkHIoAkopvKL707hRQAUUdOgoHTpigAooooAKKKKADAximEYOM04gkYFNCk9BQAlN8z2p1R0AP3cA0ZDNgiocn1NPi6de9ZJWAkooorUAoopsOCz49KAH9+v40lJGeOPWlGe1AD9y43YpmT0zSq2OCKSgBdpxnFJS5OMUyAdCTQA6iiigABIORRRRQAUAkdKKKADrRRRQAUAZOKKVeo+tAAVIOBUVTsSBkVAc55oMxsA2mTHpVkMD0qrBGPJOM96ZHKYuVoAtYGc0U2LIHmZzTqDQKD90/SiigChcIX5IzzwDXzT+2p+zVceMbOT4l+DrIHU7KI/aoIlGbiHHQAdXH8q+mWQnOQeD6VFNp4mtjHLgBh1ODivj+LOHMPxFl0qNSOvRnTlmPrYDEqUT8rLe82/K5IySAT7cH8c1aglBXLNnNfQ/7Y37JMHhu5u/il8O9OZ7Wdt2pWEa5ED/APPVAOinuPxr5tgZo38qTlgOSOlfwXxvwXi+HMwlde6ft2R5xSzDDpdS/kBSA1LC4UMR6VDFIG5yDzQj43kHv2r895Hrc+g0sP8AN/H2r1b9iXSoNY/aB0t5ySLe1nuFU/3lUD+teRb9rHPPvXqn7F3iCHw/+0DoYvpQqXIntJGPADSx5X8yK/QfDaVCnxHS599PzPmeIfaPK5qJ+g1orKiqT0HFS7cHAFRWjKQAR0GDVoAEZ3V/oplNng427H4dW+NlHyyTyf0rgfjr47t/BXgO+1i7nVDFaO5Of4uQo/XH4GvQbho4YnkJAAB5r40/b++MUV7q8Hwx0efeICJtU2N905OyPj86+F8Rc/pZPkdS8rOzPYyLAzxeKjFI+dtRuZL2Wa5f78rMxOe5OarmNTGrEdhzUkAMkR4zx1qWCJTEBgH0r/PjM8X9fzKVZ9Wfu+DpfV8Iodj1b9h6wWf47adMyZEUU7g49I8f1r79syBCGz6V8PfsEWAb4wy3Oz/VaU7fmwH9K+37b/VdO9f2z4J0lDIYs/HOL5N45lDxNOI7R+f4DmvwP/aL1Q6j8cvFVypyG8SXuD/21NfvF4zmCaJcyg/6uOQnn0WvwA+Id2upfErXdUDZ83Xrt09wZn/oK/YscrQPwjjKpaFipYE7cN/OtCyO3IHrVOyjyoOeoq5aKQ7DHevn4vQ/MYu6L1tnPSpzgj8OKggBx1+lSgbUHPWtKTRrBFZsY5qtNleTV94eMjpVK6TBxUVNWU0VsZfn1FfsH/wSMuI5f2LPDcEZ5iub1T7f6U5/rX47SyyRyA8Yz1P4V+tX/BF/WzqP7JsdgynNh4ivYOTnqyv/AOzV3ZW020fc8FT/ANqcO59esvbHevnL/goREr+AtJmIyE1g4OPVCK+kQpz8w6mvAv2+LA3fwjgukUDyNYjJz3DbxX01HSR95n0G8BM+LVXIJx16VGigPg+tWFQg7fzppthuzmuo/E5fu6/MfWv/AAT58RxSeCdQ8Os4ElrqpkAPXa44P5ivpRCFmCdMjv8AWvz/AP2YvikPhj8S7S5vrzFlco0OpD+FUJHlv9V7+1fe2iavaazp8d7aSLJG+xldTkbexz+VZVFofr/CuY06+E5eppA55Bp3BUEjpSgDHQGkdkRCSRXKtz6mbXIfJn/BQ/T4Gj0HVkjHmGS4j3d8cGvmW2jA49q+mP8AgoLqEMx0DSlf5l+0yY9iQK+aYAE/GvRjL92j8d4ls8ZYtQdD9alj71XhkAz25qUOpGc1DVz5yNhk5AGTWfd3BxgN+tW7qQAYzniuq+B3wK8R/GXxRFpdtbPFZxTb7+/I+WGEn7p9WboPQVB2YPC1MXW5IHS/sm/AC/8Aip4oi17VojHpGnziR5GXm6cf8s890HXPrX3Noen22lWa2kO1ViAVQOgAHQVj+BfAWj/D7w5BoOg2KwwW0IRIwOmP51uQIyx7247kYrKUnsfrOS5VTwWG1+IunGOM0zqfakABTdSULY97VBQTgZoooexY2M5FQ8/6sc+9O87K8LTY+G3A/rTAns8KaFJIyRS4HoKAMcCgAooooAKKKROn40ALRRRQAUUUUAFFFFABRGQYsg96Z5vuKWPdt5oAcM9qaTlM0/5vvUz/AJZ0AKnT8aWowMnAp+wepoAZT06fjR5Q9f1oTp+NAC05Ov4U2gEg5FAEgAAwKbJ2o3dKdQBGOvXFPAIHJpaKBXQUUUUDCm7X/vfrTqMAdBQA0Nu4K07t0/CkAA6UhyPuj9KAGkYOKASDkUpJzmgAnkUAJQOvXFOCDHIpsURJyRQAzysH7x/GkiOMZqSmv/q8jrigA8xe3NR4Jbd70oilIyAaWGD+Igjn0oAe/wB01DFjoB1p7YXhqjg4xjtQZjTF3I/SltcBj7GpLfhmpkGFmcj1oNCxSP8Ad60tI3b60Ga3K5Uk8MadDFjG09aWJcM2Kkj++PrWZv00HIAq7c9qjg6mpKiibANaEEo45pydfwoVVI9acAAMCgAAAGBRRQAAMCgBvzPSp90U2H+L60AlTQA+ikDqe9AK460AInX8KcOnTFNJK9BikBwc0APAAGBRSZwuSKM84x+NACMoC/SmbFp8nakOQc5oAiAA6U1XwMEVNjPGKiAHUCOgBYZfUdDU3mCXjjgdqhpYcjr6UnsA1RgYzUYaYZ5H51Mg9+lIIR3rOmAA9wakt8F356U0RgDGTTrRRtc46VqAUUUUAFJEdozS0UAFFFFABRRRQAUUUUAFFFJsHqaAFpEPf3paKAF3t60lNPEhAp1BmV7cHB4/WplfsTSlV9Kqi3baODnNAD9POYX29CKn3r61B5bbcCpIZ/MGCaDQkph8ylEg/wD1URynPf2zQAisAAmeajMeBkc+9THr0/Go1OF60AUL/TbTUrV4LuFJEkQo8bjIZT16+or4a/a5/Zc1L4W6/ceMPCNq8nh28cswjTLWUpP3TjnYex7c193+SeMCqOvaHYaxZS2mpQRTQyxlZIZFBDA9cj6GvzvjbgzCcSYF2j756mUZrWy/Ecyeh+V0Fw0J8uRuB9atROHTIPWveP2p/wBjq98ErJ46+GOiPPpZBa6sUyz2beo/vJ3x2r5+tpJ42MEqfMM59K/hzjDgzMeHMVJSj7vc/ZsnzjD4+ktdSxhjLz+VWdG1688N65aa3p8jRy2t5HOsinlSo4I/GqhlXJyaYWLJgc+9fI5Pj6uW5lDER6Hp4qhTr0JU+jP0z+FXjy18feFNK8T2dwPLvLdZJFB/iI5HXruH61102ow28W+VwMDqa+Ef2Zf2obP4S+Grnw54jivbiON/O077OMhUYfNEeflO7Bz6UfE39s74meP4prHQ510bT5ODFE2bgjjhn7f8Br+xss8YctwORw55LntsfktfhTF1MbJQXunt/wC09+19pHw2guPCvg4jUNblRlkWOTMVpkDDP6nHRRz1zXxVd3+r+IdTn1/XLpp7m6lMlxJISWJOP0qzIz3UjS3Uu5yxO5mJz+J70iQjJKdD6V/PfHniFjuKMW4p/uz73IMhoZbTTfxEFuhjV4x2Jp6KcbRT4Y8EgjvwDTIzsJB7E1+YYaPPiEj6dyXs3c+h/wDgnzp7yeL9V1MKSItOjQH/AHpT/hX2HbM2ACevWvmP/gnboW3Qtc1tgf3t5DAp9RGrMf1avp2FQnzAcZr+/wDwkwroZBTZ+G8S1FUx8zkPjTq0ehfDLW9bkbaLbTriQtnGCsZOfzH86/Am5na81Nr2QfM28k+paUv/AFr9xP25fET+Gv2ZPGWppIEYaDMFOcfM/H+Nfh2zBp2cDA9BX6NmM3Y/B+N5rnjFFvTo8LgjoKtW65DZ9fSobM5jBA+pq3bjMLfXvXhq6PzmnexLbRbRnr+NTRKcuMcdqS2A2ipYejn3pU3qdN9BhQhcE1SuIRh+M+nFXyRtwDVaf5Uy3SnfuJ7GDfPsVgT2PNfqJ/wQr11b/wCAfiTRyzbrLxdIzE9MS20LDH5Gvy81BMMzD8K/R3/ggxqqt4S8f6NvOU1ezm2nPAa3K5/8d/Su3LH759dwdUUMf6n6JMox1+hrxz9s/TjqfwP1NkjP+jPFKBjnKOMn9a9gVi4ypNcF+0Xph1b4T6/Y7cltPkP47c/0r6ij8Z+nZtHny+R+ezJ+8bnvSKu7vT3zkkjtTY1Dbh1xXY9D8MxKaqtCRExy74+D2Jr3j9lv9qmT4eyJ4K8a3jtpJkzZ3jZY2hb+BvVc9PSvC0jyvT61JHDgcDr3qFq9TuyrMMTganNTZ+mmga9pviGyh1HSdQjlhlQMrRMGVh7Grd+Y4om6/d6V+fvwd+P/AI5+El0YtLvybHPFncEvG/rgD7lev3v7dsWs+HZrWDwy1vetEVR1uN0YfHGfxrOcLM/S8NxLh6uG/eaSPO/2vfGVt4q+J95p1pIHh0wx2iENkB8b3/DoK8lij4zVzVL27v72fUr2fzJJZJJp2z1kc/y5qopO35R1HStFL3bH5tmuJeJxcpCL3+tQ3FyIyQH4706afC4Xt3rpfhH8EvHfxh8Rpp2gWRSFWze30ynyokPt/f8A6UjDB4SriqnLAf8ACH4Q+KPi14kj8PaJG2S2+8uXHywR+/vjpX3d8Hvhdofwr8Ix+GtGtNvlf6yYrzM+BlvpWf8ABX4MaF8IvDq6LoyB5CAbu8kHzzP0P4V3sR/cjjn0NZOTufquQ5JSwlPmkveHEYOKKKKZ9MBGDg0E45NFFBbVwopEH7nPtTOc0EDrYAHnv0p4i8gZ46VDbDBIqWg0CiiigAooooAKKKKACiim+Z7UAOoqOnxf1oAWig47UUAFRsd/BNO8sdzUfl+9AEtsR5Z5pP8AlnTqjyc4x+NAD4zgfjTlGTioqlg6H60Cew+msoA4p1Ncg9DQMbRRRQAVISR0Gab82dwWjzPagBw6dMUDp0xQOnTFA6dMUCauISB1NIX9BS5J7/pTWBHU0DDJ9TSDPaggg8igEg5FAElFFFABgZzigAAYFGBnNFBPKAGOBRRRQUITgZxTMDpipKQnHagV0OHUVGTyR70rMc4FNoIKbNk8N9KSMEnrn8aVcg8+tNtRknFTfQ0JVBySadaYxJntSkAA5H40tt92SlTAloopGyRxVdSFuRDOSaIPuj60Kpzkilh46jvWadzcmXv9KbD/ABfSlpIen3qm7Mx6fe4p1Nj706twCkZscClphPI9qAEooooAKcr9iabTkHP0oAawwzg+lFNbPnGn5ONtZUwF/wBv9KD8y/LRhlXrQuf8itRXQo/zxSMncCnAADAooC6I6KkphGDigE7iUUUUDIv+Ww5qePnim0UAFIY8DC7/AM6UAngUUAFFFFABTJE+UnNPooAI+IRRRRQAUUUUAFFFFABRRSBgelAC0UDp0xRQAUUUUAFFKwOTxRg+hoMxjP8A3TVSIkZAPXtU8aMhfB4OarxDZLmg0J7c4iGDSnBfg0lvERBkZ/GlOewNAEm7+LHtTAbccEn86b8/vUVAE8OSBRJBkZI5JzUgC46UNkjAoMyjNaxTRsJFUq64IYZ4/GvmH9qD9i+LU1uvG3wosI47kIXudMUALKcctH6H2719QkHGCTSSwxPGVYjHvzj3r4vifhPLuIsHKlUpq/c9PLsxxGAqqcZH5P366lpF5JYavZussbYZZAVZD6EHvxSWt6ZBuZs/Svuz9pH9jnwz8Z4JdX0ho9L10L8t6iApcHHRwO/vXxN4++Fvjv4ReJX8MeNtMe2dCdku3clwM8FW7cV/GHG3hlj8jryq0Y+4frWScR4fG01Cb94ispvlY5/i45qaJgWyPyrOtLgqm1T9c1dtn3981+RVFVhPkkfV0+Rq6LiH5cE9KmiUBsg1WV/fBp6ysveo5rF21uSlQCR6GoXwDg45qXeCvWobggqFjG7PQfyr0Mmw/t8yp011Zz4map0JSPtz9gnSVtPglbXrRkNe39zNyPvDeFH6Cvc0Q+v4Vw37OPhkeFPhRoGhyJteHTIdw9GfLmu9IIU4AzjrX+jHAWB+pZFTj5H8/wCb1nUxc5eZ8t/8FYPEP/CP/sh+KGil2tdeRbqB/tOB/Q1+OMJZ888k1+oH/BbTx3Do3wL0bwlLLiTWNdXg90hiLt+pH51+XengykYPXua9rMZWZ+H8Y1efFJGzYR4jAI7VftoTgqe9VNNVtgDjOK0YQAXB/WvMaXKfDU7iqhU7Fboc1MBhMe1MgT5TnrmlLNtweawhodEQz2P8qrzxjGamLkDpzVaclzuA602hu/QydVjBycd6+3v+CFPitdP+LHjfwdJMR9t8PWd7EhYctDcSRuff5ZF/CviTUypj5PevoL/glD43m8IftoeHbUTlYtXtLrTZgGAz5kXmoD/wKLiuvLpctRo9zhit7PMIn7QW3zKMD61jeOtNi1Xw9eabIpxJauhJ75XH9a17KQeWGYgDFRalEJomU9CPWvqaUrM/ZsRH2mDce5+Yuv2xsdTvNNBw0VzJGPqkhH8qr2sjN1bkiup/aE8Pr4W+Mut6HENqx6hJMABjCyLuH6kiuRs3/dhiea7lqrn4fmVN0MbJS7l6FhlgT3qTcQMj0qqkwYcA81J5w24zSSsc0ZroK0pz3JpIZwpcE9armQnr+FRC4aNjxxQ3Y1U2jSaYMBg54qFWJYqo6c+1P0LS9Y8QXMVhpllJcyykCOKJMsx7Djtx1r6V/Z4/YquZZ4vFfxWQLtIeDSl6L3G8/wAX0rNq0j1ssyjEY+b00PN/gR+zF4r+LGopqupWz6fpMb/vbp1O64/2VU9j/fr7K+H/AMPdA+HugpoOgaVHBFAoAUDlj3JPc1r6Ho9hotqLO1t0iRPljRUwFTjAGP5Vcx0we/FTKT6H6ZlORYbBU9fiJiBngfSiiioWrPdCijvTxjGDiqAZSbl9ahb/AFVVqDQlaGJsljz9aWwOBRaggZ9CKktoiGOB3PNAEkX3KdRgDoKKACiiigAooooAKKKKAEfOKj8/5sZFH2gnoB+dEcYblqAFp0Z4yDUG8Zp9u3lHBPWgCaigMG5FFAChTnBpPLC85p0fehlYn1oAbGTLzjHNGGBAKx/nQQR1FFADCD1A/KjLeppydPxpaAEB/dde9LRRQAUVEl0RyafCTKHIOfSgB1OV+xNIBk4pp+WTHtQBLgegoAAGBTBLk4xTs+vFAC9KKKKAGuAOgpoJHQ0rHJ4pKAHBwOMUocHrTKVeo+tAD6Cccmk+g/Sk/wB/8KCeYVSD0FKAOoFN3KOgoD+ooGr9Q8z2o3cio0HenryRQMSiiik9jMrMG7L+dNhOCT709pMA9sU2HI3kntxWUTZWsTKVY9aZbsBvA/vU235IUipoEAX8a1p7Eiw/c/GnUkUXr2paHsZjYvuU6jI6A1FGOAK5r3NCUnAzTUJEakHvTqanJ4PFbAOpwI3Z3U0deuKK0AdJ2ptOLE8LTaAG+Z7UqdPxplPi/rQAo69cU9cbeKZTlb1agAccZpoOORSliRg0lAACQcinK/Ymm04c/wB2gB1FFFBF9bhQQCMGiigsjoqSo6ACiiigABIORTl+X71NooACSeTRRRQAUUu09wfypKACiik3r60ALRQDjkUUAFBOKKKAKhOTmrEX9KVv9lf0pQoHSgzFooooLhuFInT8aE6fjS0DCq4hZXcjPHSrFFACPxH8w7VN059vSmODnOKaQe4oIe5HUxfjBWoaVs560CI4m/fTE+tNERIGRUwU56VHFaBY+etBpAdbEYqUjIwaKKAK5gzyT+tRoSUbPvVt/umq7LgECldARJCrrtHTHOK5b4ofB7wd8UtDm0LxTo8VzC6nbIAA6EjHB611UUOw/wCs/WpgmH6GvDzPKMHm1F0q0DSjXrYealB2PgX43fsOfEL4ai48QeDI21jSlOUgiH+kQL6sv8YHtXj1klxbM6SyMHBw4K4wR1GD0r9UZIEuA0UiArk9R0rx/wCMv7Hfw2+Kdw+oQWx0nUGB/wCJnYFR2/ij6N3r+e+NPBfDYtOrgVaR91lHF1WlaNZ6Hwtu2jB69qek8nrxXpvxX/ZJ+Kfwsga9t7YaxpsY/wCP60jO5R/tIOc15XdG4txslhdSPvEqRjtyD0PtX8055wdnWSVXGpDReR+gYLOMJi43jIsCbPyk1ufC3w9P4y+IWg+GbVS5u9RjjlX/AGd25j7/ACj9a5U3Sjqevf1r279gHw8viT40ya5Km6LRrCSUSdhJIdi/TjNd/h7lVXF8R04zX9XMc8xcaOWzlFn3RoVoLS3jhjXCJGFUegAA/oatySYXb+tJartQKvQDAqK+lWOFiDnr+Nf6H5RSWFwEILsfguNq6Skz8nf+C7fxJa9+Onhn4eRTkR6RoE13MgPSS4mCj/x2M/nXxbpF0u0EHtxXqP8AwU++LH/C0/24fG95ZzeZa6ZexaTbENkH7OmHx7b2b8q8e8PyuwVOfevMx1Rzrn4TxHilXxsrHaaJIWXJ61onuR0rM8PLuhJ9DWrCVxnrXLD4j51TaFhYldynrS0yOZdmwjHNDSgDrj1pW1sdMLW1CY/Liqt1KI0yBmpZZQejVQuZg0Z3H86bQkyjeyF2Z84ya1/gD8SZ/hh8bfCnxDjmeNdJ8R2NxNsP/LJJNsnfursKwb58E7Gxnoawrx5gXggbaxU7W9Djg/nRhZunVbOvLK/ssUpLuf0f6LqFvqVjDcwMCkyKyY9CAR+lXJRvDDHQ4ryP9iT4kp8U/wBmjwN44Eu433hq2eclsnzEj2OPruU5r2A4MeSeMZzmvqcPU50fvODmsTglJHwv+354ebR/i9DrcMe1dS0sb2A6tG/88V4jayDacEYHT6V9Xf8ABQvwpJfeFdL8WRw5+w30kEzY6JIPlP5ivkuBmZsbfxr1abvTPyHiihOOYXS3L9uwMYIp0VyoVs81CrTAck8d63vBHwv8dfEK9Fr4X0Oe8VzglIcKnuX9Klpni4XCYqrU5YxMPczD92OvQiu3+EH7Onjn4w36xaVpz29oj/6Rqc+4R/TGfmP0r3j4L/sL6dpZj1n4jTC7lQhhp8P+rQ+jn+P6V9FaB4f0nQdMSz0aziigjUCOKNAgUcdB1rLU+4yrhadS06xwPwT/AGbPB/wls1W3s/tV/txNqE6ZbtkKOw9+temxIkcRVO2cZ601JCGJU8Zpx8zoFNLnbR+hYPA0MFDlgh8eRCM9T606iig6BshGwjNQ9egqcxqO5pvkrQaQCIkDOe3rS+co71GZhjANNJzyaAGM2Q5H4UlSYzxioYgeeDQBPbj/AFnHSp8DOabaj9yf8adQAUUUUAFFFFABRRRQAUUVEYAeq/rQBDkgnFLGwI8oHbnmpDb45App+lK6Ahd9oxnOKj0uRi90SfTFSiFjyaTT7fa3K9TTAu2RJOSO3Wm2rZSTJ7nFSJ+7HlDFRx5Bf5etJbChoSKcHNKp6sabSgkdKYxQxHDU2lwfQ0fP70AJRS7G9KSgAopcnGKqNJxkSyfrQAjDaeDToZsH93wO+KgPnH+I0+1hOf3hOfrQBeEuBgIaam13ckUkZ+XrnFLCQTIB+NZe0diICwJjgn9aepyKYAT0FPTgEe9XTLFByM01mx9006mvgHpVANooqLyhnO2gCbax7UlLFMc49aVW527aAFzgZIpGf+6adjjFNK7VNBKsNpE6fjS9aKCgooooAXc3rSUUHjrSewFNyd0nHQGiAZCikkdtxGafbgADIrmh8QE0IG05p8EQJJBoUjHBp1u4YEkeorqASmuSOKdTX4INBmV9hzUsWQo9aTYfUVLDGCAxGPwrL2ZoIm1f+WJ+tJE2anqGIZ5ANagOpcn1NIAScCjYf7x/OgABIORTl3bePwptLvbOc0AIR5vOKSPOOPWmxkmQgDpUoB6YNADaUMR0ocYalQAilSG9xtKOvXFGF/vfpRk+ppiF8v3poJHQ0ZOMU77zZDUAIVK9DSU7Hv8A+O0hGO9AlsKr9iabRRQMKKKKACiiigAoooJwM0AFFlNuZ8jtxUUeXFSWsQ3ZyfegCYTA9F/Wn1ADg5NTAjbwR0oMypDOTk1HMx3EA/rSWCnFzwevGfrRKPmYr+FJ7DhsWFbd2qOzOTJ3p6Bj0NHl+9MsdUUcpO8enSpfrSEcYFBmZ3lkl2JOAfWrdlk7x6Go4YvkerCwgckUAOT7tNf7xpy/dphOTmgcNiSiiigsKKKKACiiigAqIrmV+e/rUtMilPQj8aCIXJntQOTmmULID91qKCwooooAZ/yx/CooQcE/lT4pCTgj8MU4jyuVoAjbDfM45+nSo4Dngt27mpo5N2T1qMW5z8qY/CgBqRbIju/CmfZg/IXt6Vb+z/uxkj6UwwsOAOKy9mmtQKcllbTRMJlUrjkFeteU/GD9kb4c/EqGS7m0RrC8bBW+siqsD6kdD1r16KAuDEQaJLZiclelfNZvwnlWc02q0NTpwuYYnCyvFnwd4/8A2BPivotzI/hTULHVbdT8qzZhlA4xnsTXvf7Hv7PmofAzw/dQ63qEU+o6i0c168I+RMDCQr6gcnPrXtTWqSliB0PT0ptvp7RcwdM5Ir5TKPDfKsox/wBYpR1PTr51iMVQ9nOWhft5XVNu4nNch8efiJZ/DD4T6548vGATR9Gnu2JPUojED88V11qkgTaVHFcX+0H8JrD43fCvXPhfqV9Law6vYSWk88QyUDkfMB3xnt6V+m+ycKSUT5XG06lXCzUdz+djWvEmoeKvE194mv5vMur6WW9uHJzmSaQuT177hWxoAbap5PTB9a+mviL/AMEU/wBq/wAGa3dW/g6LTvEOnqWFtc214sMjxgDarxuMbh9a4HV/2KP2n/htx4y+CGuRquB58OjGdD/wKFiK8Gthqsndo/FMxynHyruSgzl9CWRYsFsZ6e9aMkixLwQKkk8H+J/DyiLWtBvbYkcLPYvD/McVXnR3Ug4yD/f6VwyoVeh5iy3GU170CI3QBbcO57VCb1m4JFRzwXJPyoT9BVORZ43wwYe5FNU6q0MZYXFX+EuPcFTnNQTzLjcCOlRPcAptLAZ/2qSOz1LUn8mxsZbh+RshEjNx7IKf1epJaGtPB4t/YMzUZyjna2BWJd3REhKt9DXead8Bfjp4ofboHwq8QXW8jb5GiTt+rAfnmvS/hj/wSq/bH+J13Cv/AArWTRLaSRfNvPEN6sShTjny1JYjH071dLCVUzsw2W4yVVcsGffH/BEHxtP4i/ZDj0KaVmfQdfvLOIN/CjYlUD/vo19pY3rgHOR1rwL9g79ki0/ZB+DUXw8TVft17d3El9rF6i4RrkqqbEBP3do4Ne+Rp5SbVY8D1r38FRnTpe8ftWR0auGwUIVUcz8S/h7pnxH8MXnhbVIwY7mMox9D2P4V802f7AniT+054Z9ctIrWNyIn8ks7J2OK+ujAXQMM5p+xiAPJ6DrmvShPkQYzJcJi6vPI8G8C/sN/DHQ1S+8SSXGqSqQds42ICO20dRXsfh/wpoHh7T0sNC0+3toIxhIYo9mB+Vam19xyD0pyfdFNVHNXHhsqw1B3jHYIUCggAfhThDxnZ24p8X+pBI70dKg9JWWxXAxwKsUUUGgUUUUAOViTyaRlweOlJTsk4oAgP7rnFReX71bIPoaqFW7DpQA/yPlzj9aID0GO/NMIyJPl9anhGF6UAPooooAKKKKACijpRQAUUVXjkPm5weDQBYopFbcM4phnXOMfrQZ85JRgegoBzyKKB9RNi+lKAAMCmx8LzTqCw96KKKAClXqPrQVI6igA5HFACUdaUHJ+akoMx+RnbTCMHBpyv2JptBpAKKKKAKxUE5IoC4JOal8r/Z/Wi1hzvbb0HegBLddpNS1FDEQj59OKloAASDkU5X/vGm0AkHIoAk60U1W7GnDnmgBhUjqKSpO3T8KYQR1FACUQY5pSpHJFCw45zQA+imqygUoYHpQA1lxyKSpKjBI6GgAooowT0FAEcRBeXmmwH5h9Kc8OW3DvTDHjsK4wFUgZqsT82RUiAbs1C0mTkD9aAJIGJbr+NTrLsBBzVeI4apFBkJHp6V10wLVFGR6imSe3pTMxodT3qUHPIqAAnoKljzjj8KDQdg5xUyqcEkdqYrKGbFEJLWzAHtxQZjSDyfem7x6Gnq3YmmSdOveg0FoqOigCSH/lpTizBsCmRBlXgU8fKu7vQA0EjoaUYzyaSigB20qM5ptOVQV+tAVlPFADaAcciiigB4ORk0jr/FmkDEU5WzwaBWQw9euaKcAh6Cm0DCiiigAoqIybf3RJx60giyeJv1oAkjOVzTqAAOBRQAUUQ/8ALSigAozgZzRUMMw5KRZ470ASEg/dPWgKp9aLXc/MoxTgAOBQAUq9R9aSlT7woANpxupKdn/pnTFz5v8AOgzFoooqXexoQ24OJD+VTfSkwMYxS1FMAooorUAooooAKKKKACo6kqHyyJMxjvQAsJ5k9MVKCDyKKiMI7rQAW8zZzjNJ5GGztoteN/8Au1NQA2IYXB9aR5Bin0UAQQgfvCfwqZcbeKb5QzuzTwMcCgAooooAjphhB6mgknrTGUk5AoB6DorMgFmpbaAY5BqWPItwue9OAwMUGZCVOflFRIMyNnpk4qUwHOcUgX5ttBpo9Ct9jgdeVU+9QyaVauuwQDB7gVZhgIMhxjnipAvyjntWMkmtTnlg6L1Zg3vgXw9qseb/AEW2nXdtAmgR8fgw5rB1H9nH4MaszPqHwv0G4JHzmTRIG5PXJ28130ahhgA0q5Ejgg9BRGlSZhLAYSe8TyK9/Ym/Zj1Fi118CvDDbjkt/Y0Q/kBVMfsFfsoiTcvwD8M5Hf8AstK9n8w4wO1MyQeSaHRpGbyfA/yHmmi/sh/s36IQ2mfBPwxEVHDDQ4SR/wB9LXT6X8IPh9of/II8EafbZP8Ay62ESf8AoIFdQgycYoE6g7TG2apUKaFHLcHtyGXD4X0eJMRWiAAdCmKtW9hawR4gRR9O1XvJU/dNHkj2o9lFPQ6aWDwtF6QKgTadw61c+TOaiNuv9+k8pRxkfnWh1WRNvJOAKbwZOvFJCDgA1LSshhRRQM45pgFFFFABRRRQAUUUUAAzngZpVznikqO1mUDysd+9AFgdOmKgYeTUocd6Rjk0AQxR4O4n3qUADgUUUAFFFFABRSgkdKH+8aAGv0/GmmZemP1p9VmjcnpQA4HyRwaW3mDK6+9RYIPH6VKIWH3V/KgBUHlAc449ajUHJbPepfLnzyDSrb4H3f0oAj3t60iLhsgU/wAo+/5U6KIkdefWlqA+M4hyBUlBA6UUzMjopQpPQUhBHBoNAooqK2kIHzcigzJPMHvSjPaio8HGcGgCQN5Y570UUUAFFFIn3RQaC0yJMc570+igAooooAKKUKT0FJgjqKAAdeuKkpu1/wC9+tCqwPpQA6igDHAooAMgcVGevXNSHHeowSOlADBE3dSfxqSHG3ilX5vvURDAwKAD/lpTaMkHOaQk5x70ALT1GBTU+8KfQBG3AIqvOoLE1bACiqzQAykkiuSO4oblWirJt8ZqExgcGrGLUtuB196gjkBBUjJ7GrFuAsY4/i61utgHQnAOacxwfwoQEH8KRx81MimMimwMYprHqajp8PXFYxNLss2pwfwp4cZwDUAHYCltSDNxWxkTRseaaxyafUYJ8rI7UGgVFb5BHFIeJByaktjwT6CgCRCAOtKSMZpnnN/cqMnPU0ASRfcNOVe5FNZBHFgE/nSATDpmppgPVugzTsD0FR0/ePQ1QDSCOTSUZOMUUAFOT6/hTaKAJOlRnOeaUEjpSUAFFFFADQP3eCO1JFm36H6U+igAooo+tAC8saSlxx+7NJQAU2KPb1I4p1FABRRUdpL6igCUKSMikpbeYL1oHJyxoASil2N6UFSOooASo7Xo/wBaKSFSBx2NAEtFN/5Z06gAooooAKZFncBnvQIzswGosuo+tAD6KKKACmRYxxT6QQ+V+NAC0UidPxpaACiio4u1AElFFFABRRRQAUN0P0oooAr1Lb49O/pQYQe9IIGJBAPWgCSilb7x4pKDMG6H6VCRhMVNUL8HNBpAkVdy8/hQIwDkY/KlQHGMUpIHU0AIMKPSkZhjg0jNupKAGQZxIxJ6+tJSKuScDPNSJGepXpQAsUYxu3YpwAznHfim0fSgCSimo4OAadQAVF5H+yKlooAKEeM8Ed6YIuelJQBJTQ+BjFKuNvFKAM5FACbv9k/lTTMAcFaX5tuNtRuJPU/XFAroAT/yzpbaQ45zSxRYAJz0qQDHAoGFFFAGTigAqHB+0bRU1Q/8vNAobj4FMfBBp9Cg4xjtS7T0xQMSiio4iMvz3/rQBJRRRQAUZzzmio7XG3BoAkpkJDtgim8xM4A78U2KY44FADrcc4FS0AgjIpV6j60AHBb8aSgEg5FBJPWgzCgknqaKKACiiigAtyQz4HelYgnIpq8Z9/akY/JnNAQHZHqKqxvsNSMwxgUkYTyDk/Sgt7EsZ461MT6morcAMw75p42+o/KggbRUlR0AABPAoijCD7360+LHc0pM+PlkT8qAG4+Y4HagqzHmnc59qAAOgoNBhRh2oBwcmn011AGRQAKygelH0K0KncihG/hxQA6gADgUDp0xTX6/hQA6igdOmKDjHIzQA1vlbIptK3U/WkoAUMVpqdKdg+hoAbqKAEpQCelLt/hz70L/AA/jQAKuOWoULnhqP3lCqwPpQA2mbjndUkYwDiomwCa5wAt8z/N24quP9afrUlKi85xShoBHAMnDD86kiwV256Gm4UHNLByxAFaU92BMoIbkUP1/ClT7opHBJ4FamcCv5bDuKWL+tLT1OVrKyubNJEz/AHjUMXPT1qYeuajt8Av9K1Muo+gEHpTY+mM0kON75/CgscYMk4I/CkiiMQfcv0NOjYAnmn5U9/1oAi3Qev60kTccj3oWMk7iOlPiABINACoxlGCfpSrGT0aolODnFPtpQOSTQAEEHBoBIORSlietC9R9aAEooooAKKKKACiiigAooqusP73cPWgCxRSJnbS0AFRiUk4Bp5PGRVdxjoOp496ALNsxX5iajt5My7ffoagDMD3p+R6igCxRUUHU1LQAVFFgAY9aWolJyeT1oAkDqDkGpYZtx9frVe2QHjNT2GCXXbxQBIxwM1GZAeuaezArwahoAKdGcrmm04fcP1oAdTY+9IrBQcmiJuSM89xQAsZyv40sZJhBPrQMY4oDBjgUALUdkRw3vUlFABSbF9KWigAooooAKKKisuHy+fxoAd5vuKcDAOBUZh5wBREACdwoAkT7opaaSu3ANNoAKKdGcrmlJXqR+lK6AijORUoYE4zUSGFQd/HPemxNbsGYMOD1zWfto3E3YnJGCKdCSQc+tMBjYZDg/jToSFyPetSCSo6kyM4zSMV6E0AMo2RdSvNFKGI6UAMDAAj8qjknGcCnbl81gx61GQNmQvP0oCFxYmJUk9qasRPJpImzGwxUmVK59qC7oLddpyf51NER84qOEqFzUiSp8wCqMCggb5JzwT9KPL96cLglfujp6Uw3O3rs/KgTkxIcwjAqSoS6letOt2BBxQODJKKKKDQKjqSoTAcZAH5UAPtzgyEmkDgjaKavnBcbcClSLjPH0qftASJ0/GlyR0NMRByBz6VJDLtU7h0ODmqMwYYOKSpDKG4C1HQaBSb19aTzPam4Gc4oALfoWBqSo7bKiQH0qXjHvQAbjnOaXdkY9qQg+hpKDMgZcHpxSRjYmG9RUhHYimIpLyY9OKDQfCcs1AnPcUkMW2Mkj8KQtGp2gfpQA7zxjpTRIB0GPpRGcM/t2pylTyOlADCZe36iktozn5vSpDjtTNjelAEkP3aeDg5pByM4pvmjd1oAfRRQTxmgzCk3qTgUwS88N9KVV3UASAEjd1pACegp0OGUA1II1wOaAIl4PPcUzyx3NSOB1qJiQ3BoASNME5FNEC469aehAOSaj+054DD8KAAFirgCpLH5I2z61FHIOSD+tSQMcSEUXQ7MltgdhLcc00R/Nw1NWUAfeqRGRsdM0DurApAOTSUo7fWkoCJIBgYopof1FDPg4AoKHUhBI4NJu+X3oVs/KaAFAwMGm5Oc0+igBFbPBpNyjoKPmVaaM54oAkHTpimsWH3RSBivUUobsq0C1Da/979aQBsZApSzDtTRIeQFoBO45f7jU6o+lPVtwoGIE9TQoIbpTgAOBTd3ze1ADqAAOgpv3PfNG8dNvFACEAcg1GwwcU+mM27tWGlwGbD6ilUYFJ5oB/8Ar0qnIz61kJ7CKAWIHXNLaf65/rToIwzMTTkQqePzrrp6ogWikT7opaYLcr0+H71O79PwqJ+FZveszbmJkxukwafar+6cgc1AkmW2mlb7tXfS5lDqSHAL/SguvagY8oY9OaYDkZplhFnzX+tAJH/LUUVHSbsBLDLF3PP0p9PBGMimUwDyv9n9ajPB4NShmP8Ay0WnQ9MEdBQAygdeuKKASDkUAFFLxjp+tIAT0oAKKKKACiim+Z7UAO+lRDqTTjMB2/WmxYOCPWgBwYpbsc9zUC3BxgNirR5GDVN4ZQSQeM9qAWhznxN+J/hr4SeD7jxv4q1T7PYWsYMpkUsQcjA25ySx4HpivKPhH/wUC+DvxX8ZxeALGLU9NvLltto+qJtWdiBhVYMQGPYGm/8ABRm0a4/Zq1KRj/q72zbn/rqK+F/2ewYvjv4WePq3iazIx7yY/lX5znnEGJweaU6EHpJ2PCxeY1aOLVNbM/WqF1eIFaUxEdue9JZD/RQxGT1qwwyeO9fd4aftaKZ68dirxjr+NFvLsyRzSG2PlkA5xUeDboWFdZsTwXY+fn0pkLAyPg96flEQHcMkZpnme3JoAZUkSBRkt+tMJ54Y0iyMT8uaVkBajOIwfamsePoKYPPHQj86chJUZpgOh+7SSSELhTgUQsACDVfULqC1s5Ll3+VFJLZ6cVz1KnsqPMyZOyPMf2gf2pvA/wCz5ZRP4gS5uLq6c/Z7C1wZGAwGc5PC54FZv7On7XHgb9oQ3Fr4cS90+7sUSS60++UBwjcLIGyd6kjGAeK+Iv2t/ifN8WPjZqer2kxlsbWX7JppRiQYom2sevRnJNUf2W/ijc/B34zaZ4tnyto0v2S8XdhTbS4DE8/wsVIr8w/1uqrOPZX9y9j5v+128Z7Ppc/VG3lDxg5zx0qUMo4zWfoF/b6jYJeQSBlZQSw6Hp/QitHYgOeOvrX6hhasa1LmR9HzPlQpHzYFJSn73XvSVuIKKKKDQKKZF/Sn0AFIxIGRS0x/vGgzIbcnex96kY4BpsKEMT60SMBSugIkc9cU4TseAwFRBxErMxxjJ54rxf8Aaa/a98LfATS302Af2lrjj/RtLiYAjJ+9Kf4U/XFeZjsfQy+i51Z2M62JhQhebPZdR17S9AspLzVL6KGOMFpZJ5Aqr9STwK8U+IH7f37Pnge7l01fFo1W6jJDw6VG8wBHYtnbXwf8Y/2mfip8a9SZvGHiyZrYHMenWpaO1iHTGONxHQlutN+GX7PPxe+Lkiv4J8H3c8HQ3Tx+Rbj33v169QK/PMXxhjcVV9ng4Nng1c3r1JctCNz6c8R/8FUfDtrdGHw98MtQmTBw9zqaRA89gAf1rKh/4KyFJTFN8JXKjP3NdU8fjHWB4Z/4JbfFfWVD+JPFmlae2MlFhkuGH48Ctuf/AIJN+KI8fZfipYO38Qm0V8H8Q9ciqcWVFzKLM/a5xLVRO18J/wDBU74Uaika+KPCWs6XkgNN5aXKL7nYQT+Ve4/DT9o/4U/Fi2STwP4y0++YoC0EcxWZB7xths8elfFXxB/4JtfHLwjYSahoUena6sYysWnSuk34I+AfzrwXVrTxT8PfEX2W4ttR0rU7N84lR4Jo2BPIPXP0rop8Q51lrti4OxUcwx1B/vYn7FW96HjxCwOBz/ntViGRnH3c18Afsuf8FH9b8O6jb+EPjdfSXdkxEcGtbMywDoPNX+MZ/i6192+FvEOl+JdMi1TSr9J4Z41kt5YnyrqcYYHvmvuMozvDZpBOEvke1hMZSxUbrc2Ni+lMji6kGpKYAeucV9EdkSuBmUg9jXD/ABl+O3w5+CWiJrvj7xDBZwyy7IUBkaRz6BFJJruCCkmV65r4f/4KoyXK+JPC8e8geReMvswI5/Wvn+Isyq5bl0qsN0cONxMsLQlOJ6uP+ClH7OPEZ12/wRyRo0/+FSp/wUh/ZuY7R4ovRx30if8Awr4Z+D/wa8Z/GXWrvQfBGlC6ura2SYxzXYjAjOBuyTyc5rvV/wCCfP7TqSEt4HtyO23V4ePzNfmuH4k4ixUeejTuu6ueLSzLMakbxhdH1Yn/AAUl/ZsjG0+KrzP/AGCLj/CpLb/gpJ+zNIdkni27X0LaRcf4V8nSfsB/tKINreB93+5qkOR/49UEn7Cn7ScMOD8PbpuM/JqUJP8A6FXoRzjibrS/Mp47M0/gPt3wr+2t+zl4xdLfTfihp0UkpARL6BoCc8fxgD9a9O0zXdL1SJLrT7yOaN1yjxuGDD1BBIr8tfGH7L/x98HW7T6x8NdaW3QZaVI1nVQO5CMaX4N/tC/Ff4F6oJvDWvXH2NXxPpl+zPA4zz8pOY2xwMYxXZhuLcXhpqOMpOPma080qxf7+Fj9UhJuDFlwB61JagZBI7da8f8A2Zv2mPDHx58PC/0/NpqVooXUtMmbc9u3XIP/AC0U9jXr8J3RllHavvcFjqGYUFWps9mhVp1Y88NizSNyuaYHzDgnnFFeibBRRRQAhIIIBFQE7en4E05VIDNnvVXVbyKy0+W8Z/lCZGT04/z+Vc06vsqbqSCTtG7PNf2jP2rPA/7OmnRXHiGC5u7m8fba2VmRvYjqTk8DjrVb9mr9r3wD+0ZDcW/h6G6s7+yiD3Fherh0RuA4PRgea+Dv2s/iZL8YPjXqmtWt00lnaXH2HTArnb5URw5Hsz5P4Uz9ln4m3PwW+M+j+J7mQpaGUWuoAZx9mmwrN1/hYqw+lfmUuMKrzlUU/cvY+c/teX1zk+zex+qVvJuXHfFTRHJP1rO0a9S+sUuYmzuHLD14/wDrVcj6j6+tfplGrGrGMl1Pok7q5JRR90fSo1OMEV1DHQKCr5pxzjiiAja4DDk0fWguGhj+IfE+neFNDudd1y7FvbWlu0s8krcRqo3Fjz9K8I8Of8FMf2fNf8Yr4VN3qdqkk3kxalcWbfZmJIAJb3yOfeu6/bEBm/Z18XHj/kX52IPsFr8tbGPbqStzkuvf3Ffn/EXEOJy/HU4U9meHmGPq4etGK2Z+zNpPHcxCVOQR1zmnxjDk+prN8IM39gW5YnJiQYz7CtNCd2a+xwdV4ihGqz2KWsEROD52QO9RalfxWFpJdykbY1LMT2AqdsM24/yrK8Zx7/Dt9Gf4rSUfnG1Vi60qNByRc9Itngs//BSP4BWfiyTwk+o6m0MU7RTarHb/AOjqdwzgk5ZeeuK+gPDfiDTfEui2+uaNeR3FrcRLJHLG2QyEcNnNfjlcwDzQy/eEaLuH8OGIxX1n/wAE7f2pl8OXkfwM8YaiVs55ydDuJX/1bHOYCSf4v4fSvzvJuMZ1sxlRrOyvZHgYPN4yxLpTPuy0+7tx0pcZzUFpIZVBiJ5H5VNEMkgn6V+nQlGcU0e9uriDIIPrUexvSpxkjJFMbOeascdiPccYzTZ7qOC2L44VDmlcYzxVTVyfsEiqeSvFcmIqujRlJEz0TZ8/eNf+CifwW8FeObnwTe/2pcpZ3Jgu7ywt98MTggMM5y+Oc4r3nwh4q0nxjoUPiTRLpbm1vbZZYJ43yGQgFSDn/Jr8iPHwZfHurOxOV1m9IxnjNzJmv0y/Yat0h/Zh8HRjP/IFjwM9i5r4fhzPsTmGZVKM9k/1PIwOMlWrSi+jPY1GBSM7AkA0oGBg0j9OlfoZ7ZAGKbiT6kV4r8SP26PgT8MPFEvgzxB4rd9QtWKzRWlrLPsbjhivGa9l1MFLNwrcsp/Cvyc+Pdi0Hxx8U2skhBHiG4IOeh3jH6Zr4zirO8Rk9CLoq9zxszx9TB0rxW7PtuX/AIKbfs7QMyyarqr4/u6LJ/jSJ/wU7/ZykXdNqepxg/39Gk6fga+Qfh9+x78aPil4XtfGXgvQra7srwusBfUBGflbaSwPTkGtOP8A4J6ftQElG8EQnBOM6vF/U18nRz7iWvTU4wun6nnUsbmUo8yhofVjf8FO/wBmArx4g1HPto01LF/wU0/ZpLbU1nU+f+oTKP618qD/AIJ7/tRDgeBYvr/bMP8A8VTl/wCCf37UydfBEfHpq8P+NW834m/59fmaPG5qvsH1Wf8Agpj+zcD/AMhXUvb/AIlkn+NPT/gpj+zMyjPiO+iPYvpk3FfLA/YA/afaPnwVHnuP7Wh/xqM/8E9f2op2KjwOgye+qw/40v7Z4lX/AC6f3MyeNzVP4PwPvz4OftCfDH42acL/AMBeIob1OkgQlXUns6tyCa7n+H5e3evlz9gn9lbxz8Bo9W8R/ECRYrvVI4YksIZfMaGONs5YqcEsWPToBX1Gc7Tj86/Qckr43E4ZPERsz6DBTqVaKlVVmPAzwBzSU4EKvy02vcOuF0FOQDGaaCQciigCSimq/YmnAYGKACmMMHrT6Y/3jQLqJSgkdKSmYJk5NAPYfRAcGQ0saAA80kZA3e9BAr/eNICQcilYgnIpKDQd5ntTQSOhopR65oAO3X8KMn1NJRQAVE/3TUtRt0P0pPYCPJHQ09eFGaZQgDMMetZR2AsAAdBSqcGkoBxyK2MwooooBbkdH0qOkslJPTvWZoXQO1UWBzuFXqrP16fpV9DOAhmz1Pan/Io55zzTAD3H6VJHuMTfhTNBwhBGQaYIR3NT1HQAnlN/z2paKKADIPQ0RE+UDnvTUyBn8qWKLHGaAFooooAASDkUUUUAHGKKKKACmyEBeakZcL16VAxbPz9M9xQA4dB9aUHJFJHje2OlCfeFACsxyRmmykiPg9qcxAOVqOVttuxPoaDM8I/4KHbn/Zh1s4xtmsj/AOR1r4P/AGefm+O/hIEf8zLZH/yLX3n/AMFBhn9lvXF4/wBZacn/AK7rXwl+z9AY/jp4Vkz08R2Z/wDIpr8Y4nj/AML9J+f6ny+ZR/4UIfL8z9YtOObZfoKs1T01yLZR7CrPJPHev1fAf7tE+np7Eagb3wOT0qLB64qcx9zmoj/q2UetegV7SxDRjPGKkEDHnNPtlOGyPTrQWMjgON1OtosZBWrFoAIZSR2pjID0oArhGz14+tSKoCgk0vk845pdhC/QUARxtxjPHvXjv7ZfxeT4T/BzVL2G5WPUdQzZacN2D5rqAx69AM/TNewyFUi39sZ/Kvz5/wCCj/xIuvF/xfh8CWN0Xs9DthvCsCPtMnzE/gMfSvkuKMx+pZa0viZ5mZYj2GFdtzy34OeAr34qfEfTPDdlCdlxcL9oyDhYEyXb9PzNL8ePAE3wp+I2o+FpoWWGKUtaPjHmQSD5X/AZH4V9If8ABN34Syvaap8SdWtcF1+w6bIw6qOZG+hJxTv+ClPwcNzodh8TtJtsGzk+yX7gf8sTnyz+DDFfmcMln/ZLxrXvXufOrAv6r7brues/sF/FKT4kfA3TWv7vzNQ0p20+/VmyS8ZGxj6lowD+Fe3BcgEGvz//AOCavxSfwj8T7jwBqEpS116DMW58f6VCCR+LLuH4V+gEDpIgCdDjFfpvCmYLFYCKe60Z9FluKdfDruiaiiivrDvFAycGkjO0cilwc4oXOfloNCM4hp9IeI8nsOtMQjJ2HPrQASqGPWo7cfJJ/vVYQ7oee9NBwCCKXQCBk3DB/Q0k5WOIbecDrSnKvuA4zVLxFqlroWi3Gq3lwIoY4WkkdzgIApJJ9gBmuWrUhhqLkyZNKNzyf9q79obT/gJ4Fl1GGVbjW75Wh0mwd/8AWPgjzG/2Fx+fFfnJf6/4j+KGvvqep3lxe39/MDJK4JeaVuQAM5HYBenFdn+038Yrn46/Ei68SLO39nxu8WlQs3+rgjOAf+BH5z7Yr37/AIJ2/szwTK3xv8Y6VukDNHocE65AAP8AryD1yDgGvyHMq+J4nzf2FN+5E+TxE6mY4r2cPhRofsrf8E/dM0+ODx38aNK+1XrqHttFkwUtx1Hmn+I+3avrbRNB0vRrFLPTrOKKKNdscccYUIMfdAHarFta+VEFQHgcVLEsgYk9Pev0bKMiwmX0VGMde59DhcJRw9JKKFjRWXnr2zT1iyGOM460kI2klh+lPBOJB7V70KUYqx1dCB4UcYcZU9civL/jt+zd8Pfjdor6Z4q0WMSqCLPUocefASMA7sZI9q9TKNjr+VMNupGStcOLy7C42k4VI3uZVMP7aPLLY/Kz9ob9lXxp8BNZ+z6tp01xpzv/AKFqtpAzpIM8BgBw2K+2P+CfNj4r8Pfs/aTpHiizuIn82WWzS4B3RW8jgxKc9OMn2xXt95oWk6lBsvLWN13crJEGGfXBFWLCytrGLyIIAqjoFFfN5Xwv/ZmYOpCXuvocOHy+GHqucWWFck4Ip1FR19uekSOAFGAK+Hv+Cqu0+KPCYOM/Zr7/ANp19uliFIr4i/4KoRlvFPhRhwBb33/tKvjeNFfJZHmZv/uMjnf+CXQV/jPrvm4P/FPgKCen76vv6GCF48bVxXwB/wAEuUH/AAunWVK5/wCJCP8A0aK/QK2hwjydivA9K5OBqcJZXFNEZN/uiGNbwkHEY5/2aaLWE8eXx/u1a8vgEmhYgec19v8AV6XY9WyKEum2s6fvIlIPUGvl79sr9kHRvEmiX3xC8C6THbazaq09zbRKAt6gXk7R0fv+FfVe1lbpnmqmqafbX1o8UqD51O78ua8fN8ow2Nwri462OfE4eFalytH5S/BX4uaz8E/iHZ+NNLmkAs7jbcQ8/v7fA3qR3YjoPUV+o3w+8V6X4y8MWfiTR7kPa3cCTwMD/AwBX6+h+lfl/wDtPeEbLwB8aPEfhnS1VYrbV3aBUGMK6rKB79fyr7R/4Ju+LJ9c+AsWlyEv/YuqT2GSc/uwVkT9Hx+FfBcIYuthMyngpPRPQ8TKa0qeIlQex9IDpntRQhJUbfSlGM8iv1pO59IJRSeYv92jePQ0wK7AlshsYPWvGf21PjHD8I/gtqFzbSbb+9BsdMQnkyOPmf6Dca9mnYJGWPTqa/Pj/go/8TZPGXxYXwDauWt9AgCsVbI+0OA7fkMD2r5PibHrB5c0t2edmNf2OGbW7PJfgR8PdS+K3xL0rw5aKRHLcrJeOcnbCh3SMfr61Y+PXgG7+FnxI1Pw1coRHFMz2px963kBKt9QP5V9J/8ABNL4SM2m6v8AEnU7LaZX+wWEjDqikGU/Qk4qf/gpN8FjeaJZfFPSrYbrY/ZNRfHWI58tvwPFfmSySayl463vN3Pn1g39T9rbXc9a/Yf+LK/E/wCBmm3Nzcb7/Tk+wX6E5PmxkAE88lkANezwgKyqCcDpX55f8E1vi/J4O+L03w41G42WviKA+QWbhbuEEr+LruH4V+hdo4cjb3wRX6Twrj3jcuipbxPo8sxP1jDK+6LIxnkUwn5sg04IcfLTK+wPSCnAkJk02pA37gYH4UAeWfteZb9nfxeD38PXI/8AHRX5bWZxfRE/89UIx/vLX6lftaqG/Z58WA99CuB/46K/LezgZtTto1zkzxjj/fWvx3jJ2zOl/XU+VzhWxNM/YTwaT/Ydsx4IiXr9BWuhyGNZfhVSNHgT/pmv8lrSRiNw96/T8s/3GJ9HQVqYrdD9KyvFZH9kXUZ7wsM/VTWoxwh9hWT4vYjRblR12HB/4DV5p/uTZpP+Gz8fL+EwXkw3ZVXbcPo7VHqNnrnhbUYLrMltNGIriKRGwQrAFJFPc88e9WNT5vZ+efMlx/301fYHxA/ZRh+LH7MPhPxn4StVPiDT/Ctm6qF/4+4/JBaI+rf3a/n3CZfXxmJq1KPxQd/xPg/qkqlWc4bo9Y/Yh/aatvjf4ETTNevFTXtIRYdUizjzAPuTj13jr6EGveY2Csdo4PK8V+Snwf8Aih4n+A/xCtPFmis0c9lIUuLWQkeZHkiSJh68H6Gv1A+DPxW8N/GDwTYeMvC10JLS8i5Vj80TjG6JvR1NfrPC2dLE0/YVvjR9RlmNVakoy3R10R3Kc0MpJyKkjjUQgKc8cH1pF5ON2K+5PXIqr6uuyzfA6KSatKuTketVtaUG2lH+zXFjf91ZlW+Bn48/EVseNdXbjnVLz/0oev0z/Yccy/sxeD5Fb/mDQgf99GvzL+IyMvjjWFHbV70f+TD1+mH7CLEfsveD/bSIv/Qmr8o4Md87q+r/ADPm8q/3ufqeweaeKdTUaPA3R5/CnV+xN3R9SVNRObaT5q/KL9ph3H7Q3i1Acf8AE9m6f7wr9XNR4s5TnoDX5SftLKD+0N4uJ/6D0v8AMV+Z8fq2Gp+p89niTpx9T7k/4J1wq37NGhuVHFxeDJHb7Swr3yK2hk6IPyrwr/gnYmP2aNDP/TxeH/yaevfLcAE4FfV8PUacsrptrZL8j08FFfVYkX2aH+4P++aPs0Xp/wCO1MTk5FO+X+9+te59Wo9jr5IFcW8XQR/+O0CK2A4X/wAcqwAFFQr1zimsPS7CaiNjiWJuOPpUoJHQ0m75ttLWy93YuKsgBIORSqMnFJzjOKWIYoGOy/oKZUhOBmoznPNAACR0NORv4cUn8XzfjQp2tg0APprfe+9Qr9iaaASeBQAdaOc0vKmheo+tACQ8MxBPWmhxjmpLTG7n1qNRhW+ppUmwFT/VNS0UUwAEg5FFFL26/hQAlFFFAEY56ChQJOBT/wB971FDMT2+uKWjQCP940W6kkEetGG64/SlgByMUwJqKKUdeuKDMSmecpOBT6hiY5Gf1oBbjWPUio4mEZkbHftTSDk8VLa9PwrHmOgsEkDgVFanrmrPUA1BbgE1sc45Cc4ogzl93rS8uTkdKFAHSktjQWiikh++1MB2OcZ/GmmMdjS0UAL/AMsxmkp8cf73haZQAUixiPilooAKUEjpSUUAFFFH0oAPpTZfu/jTqOtAEXmLilUgjn0qExJjJP60KSGGD+tAD4C2SafK48huPWmQdD9aViTATisY7AeF/wDBQIeZ+zFrw9JbQ8f9dlr4U+AEu/4z+Fz0J8Q2XP8A21r7w/bxgWX9mTxCrH/n1Of+26V8J/s+WmPjX4WBfgeILLH4OK/JOK7f29R9V+Z8tmKbx8H6H6saeNsKD2q0eg4qtaEGIKKlx/FnvX6jgVbDo+jp83Ix9FPtSCWJplegUFAOORSJnHPrS/WgAC+n86KUA5xQVIGTQaCU1mJXg/jTk2g+1NdxszGR7VL90zuzlfiz47sfhx8P9U8Y6jIPJsLR5ypbH3RwPqWxX5c3+p698UPHc2oupn1DWL/djrmWVsKMdsZx+FfWX/BTr4uf2X4R0z4V6fcES6pKbq+Ctgi3ibAH0Z/5V5B/wTz+GEvjr40x+Jb+28yz8PqLmR+zXDkrEPcYy35V+RcR4iWaZ1DCwei3PmsfUeKxkaC2R9z/AAN+HVp8L/hxpfg62T/jwsVjlGPvPjMh98mk+M/gC1+Ivw71Lwlf2+9NQsWiUEA7GKgq31Dd67C3iMUKqvIUDB71JNGJYChXquOe1foP9mUo5X9XtpY9yVCKo8i2sfkho2reIvhX8S4tRtpGt9Q0TUvNMafwywvgg/UAj/gRr9S/ht450vx74TsvFGkSg217axTwYP3VkAO0+4KkH0r4I/b9+ETeAvjdc+KNMtylj4gVblCBgeenEgHucBq9o/4Jm/Etdc8FX/w11CfM+iXImslZ+fs0pLY99sgP0DV8Jw7iJZXnM8LN6PY8bLJPD4qVJn1lbhhg5Jqz/B+FVrYkxj5e1TwE+XlvWv1enLmjdH0khwG0dO1RxSdjmpaKoTdyJz+7f3HamISv+qP6U5ySeacBgYoLEJIT8KZ1Qn2pV3A5waUKSMbe1AEKylRkH9K8E/4KA/E6bwH8Dr2xtbvZd6zOthEwPIVzmQ/TYMfjXvEnzH8a+H/+CpviDd4j8O+F45PljhursrnoSRGD/OvleKcR9Wyqcl2PMzGq6WGbR86fCXwS/wAUPH2leDbIFRqV9HCdn/LND9849AikV+q/gjw1Y+F/Dltomm24it7S3WKCMD7qKFAA9uK/Pn/gnB4VbV/2g4tSlBePTNLnmwD91jiNT/Ov0htkEMSg8AAAE187wDg4Ok8S92cWS0kqLqdWSUAAcCiiv0w9wcp4JxzSBuDjHNJUQcKST2NTJlXViUnHJoqPzQcAelBYHq361j7aHcFJMkoqIyhQf1pFk3DKvkd8GrjUhJ2uSmnoTVHTgcnIX9abWoDFYlcY618Tf8FTgT4h8LMT/wAsLzt/1zr7bIAXAFfE3/BUz5vEHhbA6W96f/RdfG8af8iWSPLzbXASMD/gl1EB8Y9akxwNDUf+Rq+/YnTbtHGRXwJ/wS/YL8Wdc/7AqY/7+197RZJVs9q5+A7RytIjJlbCIt4GOvakU4OaaWGM57UKRtBzX3R65CXY8k1Xu5EWB2JGNp79OKkBUEszAAdfauK+NnxQ0L4UeA9R8Xa7MqpaxMxjzgzSHHlxgdy2APzrz8diIYTDSnN9CK1RQpts/Oz9uTUIL79pfxULYj5LuFGKf3lt0B/HNfUP/BKqOdfg3q1xKTiXxJPsJPXEaKf5V8P+LPEVz428W33iXV/3l1f30lxcEZILOd20enQJ+FfpH+w/8K7j4VfAbStI1KErd3IN5exkYKyzFHI/AcV+W8N054nPqmIWx87lkHVxkqiPbEB8v2xxSfSgcDFOwCu72r9dpn06WhV6U9Zdgz1wO9MJBJ5oBO7g49zTloUcx8X/AB5p/wAMvh9q3jPUnxBp1m85BPU44X8WwPwr8sZ9X1/4n/ECa/KNNf6xqBYAnOZZWwowewzj8K+wf+CnHxSj03wXpvwpsrnE2pz/AGq9UNyLeI4Uf8Cf+VeNf8E9PhJL45+N0Pie9ty1j4excykDhp2JWIe/Ut+FfkfEVeeaZ5TwsHonqfK5hVlicbGjHY+6/gV8NLX4W/C3S/B1og/0LTljkyOWkxlz+LVY+L3gOy+Ivw+1TwbfRB0v9PeAAgfK5XKt+BxXWW8YgjWNP4QAPWlnUSxmPGOMZxX6H/ZlKOWfV1tY972EI0ORdj8e7WTxL8LPiomqIWg1HQ9VEoQcbJYXww/EA/nX6t/Cvxzp3xA8G6f4p01wYL+wW4ix2DDkfUHNfDH/AAUM+FMHgv4zP4r060EVnr8IuRheDOp2yD6nG6vWP+CY/wAUX1zwde/DHUZ/3+iXHnWW88mznB49yr5Htmvz7h+vPKs8lhJPRniZbL6ri5UWfXChfIByc7RmkZABkUIf3W0dQuKEYOME1+uQ+E+nG0xWYHn1qRSAckUwuemKoDzP9rYH/hnfxaB/0Arj/wBBWvzH0pAuq228cC6h/wDRiV+nX7W2T+z34rx0/sO449sCvzGtYXbUoUTOfPixj/rotfj3GTX9qUv66nzGbv8A2qCP158MD/iWQgf881/ktaAwu4e9ZvhYkaRbBh/yzUcH/ZFacYBLEe2M1+n5W/8AYon0VH4CJs7jmsrxcV/suct0CjI/CtkgZzisbxhtOk3YzzsHP4VWYq+CkOo/cPyBu3WSeaUdGaUjA/2mr9T/ANm+0B+AfhJOOPDVlyf+uC81+V80LxIyOeiy9Pq1fqv+zcw/4UR4UDDp4asv/RC1+YcGU4vMKy9T5zLUpVpnyD/wUR/Zdn8MalP8XPBdjtsbqUHV4UT/AFb4x54AHQnOfeuR/Ye/an/4UX4zbwx4tvHTw/rEoS6kJJ+yTkkLcdeARw2O2D2r9C/GXhLTPF2j3OhatZJNBcQtDKkoBDoeo/nivzX/AGq/2YdZ+A/jFksonk0a9Zm0q5PRVIOYm/2gD+VdWe5dXyrFLF0NNRYzDTwlX21M/UDS9Tg1O0juYJgVkVWUo2RgjIOfQirbHnINfFv/AAT9/ayi1KOy+BPjnUD59spXQ7mVzmeMHIt2J5Mi4O3/AGa+y7a48+MONvze/wCh96+1yLOKOY4ZP7XU9zB11XpKSJY+xqtrjBYJP92rKEoAPbrVLXji1mx+Feljm/qsjpqJ8h+Q/wAUY4/+Fi68gAGNbvcY/wCu71+k/wCwqqL+zB4Q/wCwPH/6E1fmv8T2dfiFre49dZvD/wCTD1+k/wCwuCv7Mng7Dk50lMZ/3mr8p4MSWc1vV/mfOZXrjJ+p7AvOM05go4C01OcYpx65z+Ga/W27H0r2KWqf8ekn+6a/KL9pJm/4aF8XnH/MwT4/MV+rmrHbYzHtsPNflD+0iCv7QHi3gf8AIwz9f94V+e8e64enfufO547U4vzPvH/gnmNn7M+hdP8AW3Z6/wDTy9e6xTMZCM8V8nfsVftD/CnwH8CNF8M+L/iRpGn3tt5/n2t5drG8e64YgEH1BBz6GvXB+2X+zxCpL/Frw93wRqKn+Vezkeb4Kjl1OMp9vyO7BYqgsNG76HqbXDBiPej7S5wMV5K/7a37NYbB+LOhnv8ALeZ/kKhn/bi/ZnjHz/FjSPwuT/QV6zz/AC7+f8jqWMw/dfeewG4k+8CcVGsmO5/OvJIf24f2apfu/FnRBk4+a6P+Fdf8Ovjf8M/ilavdeBPF1hqkMLhJWsphJ5bHGA2cMD6VpQzjA4ipyQnf7jSniKNR2VvvOujODkH61LaMGdjnIxUMIwv3u3WpLHvz2r1YtG5ZAAGKaSFONopQQeBSMGb+GrEtgJZh92jy/ehVYH0ptAx3l+9H/fVJuONtKhOcUAGw+ooK7VNOAAGBRQBHSgkdKeQCMGoznvQAVHGMfdqSlXBOCKAEop3l+9Jg+hoAACegpOnQ1IAAMCmsrE+tADaKd/tb/wBKbQAxpB0ANR2xAPNSs+RgVDa4y+KT2AlBIORSRYyeOlIhJHNNtTkucdDWNBNsCeiiitzMKhfgAVJ5g7io2ORkD8aBrchpYAPLBpfLPc0tt1Kkd+K5FuWWd/GNpqOEcZqxkeoplquK6lsZjlzt5pCX9KRZB0FLH+64OPwphAbUlR0UGgUUUUAHGKKdtf8AvfrTaACiiigApAbgdzRmbOOaXLd2pUwCiiimAUjHApaQluwoAj8hDwDUa2+KfGJ8cwmpdi0AQxYj5zSsQYSKdhkiJWmy5MZxzxQJ7Hif7duT+zX4gPYC0/8AShK+F/2fcn44eGMjH/E+s+n/AF0Ffdf7eg/4xj18qBwtqfyuI6+Ev2fQz/G/wyqnJ/4SCzGR7SD/AOtX47xUr8QUfVfmfL43/f4H6qW0e6IYyMDtTskQf/Xp1hzCAR2p4UE48j9K/VMH/u6Pp6VkgjHl9v1paBjOSKK7iQooooAKUgheTxSQKCH+lK5Aj5PagCuuc8VX1HUoNPsJL2aUKkaElieBx1PtUzkY3K30NeIftx/FaX4a/B27gsrvZe6tILCxGcFAyjzD74AOfrXjZrjPqWAlVl5kV6sKVNvsfEH7U3xKj+Lvxs1jxFDMzWpufstidxIFvCAit9CxLZr7R/4J/fCKb4dfBqDVb+2KX2uXBvpg3UK20RL9NmD9a+Hfgp4FuPib8VdL8KpGBFcXqrIWI+SFSWc5J6bQB71+pGgXOlaRpcFjbyxxxRIqxIGA2qBgAc9MAV+a8LQhi8wnjKz6nz2XQjWxMqzN2MgYUDt0pzYIIqiNe01etzFn/rqP8aafEemr/wAvMZ/7aj/Gv1H6/g+X4j6H2lNdTwv9v34ZyeOvgrd6/Y2nmXehXBvYAMZ8ofLIPyOfwr4y/ZS+MA+Dnxx0zWr65aOynlFlqZB4EErBd3/AWZD+Zr9KvE8ukeINDu9HvGWRLiF45BkHIYYI6n1NflV8Y/BU3gPxzqnhplZG0/Unj2n7zRblIPudor8w4o5MLmVPF0n6nzuY2o4iFWDP1y0yZbq3WZV4x25/z2q2JQQCp6DivDf2G/jFL8Xvgzplxql4z6lpu2x1HLcmSMDax9S6YavboW3qSAM+lfpOUYyOKwcZx6n0VCp7ampId52flY02iivYN4EgGBigRDG7caQYwM+lReWxOSf1oAmYdRRSv940lBmVXIGQTznivz5/4KcyvJ8erCBm4Tw7Ftz0yZnz/Kv0GwGyV9a+Ev8AgqB4bni+JOieIEg+W50h4fMPrHMTj64bP4V8TxrGU8qkkeXm6/2R2Iv+CXEcQ+Keusxw/wDYiYz6efivvrIMQAH0r87v+Cbmtx6Z8e30mRuL/RLiNAT95kZJB+OM/lX6HwsWgyRWXAso/wBnKKIyd3wkUTE4202lycYpK+60aPXITKUUsO1fGX7YP/BQP4g/B3403Pwv+HuhaeiWMEb3d3qIklE8j8gKqsNqgDv3r7LKliQBXinxu/Ye+DHxy8Yjx54nsLtb/wAoQS3NlfmMyqCOGBHJ7Zrws9oY2thuXDS944cXDETp2pux8oW//BUX9pkD99a+GGGP+gZMP/alW0/4KlftCYAl0fw0x9rOcf8As9e/2/8AwTD/AGdQoR7fWDx0/tU/4VOP+CYn7N/Q2GsH/uLNz+lfDvKeJv8An4/vPK+rZl0mfPP/AA9J/aAEpV9E8OYHcWk3f6vXo37Lf/BQ7xf8R/iTY/D34heErMHVpTFZX2kFkWNyudrox64HWqH7TX7Bvwb+FHwg1bx94UbU4b7TI0miNxfeYr5kVNrA/XNeD/sf26/8NLeEOOBr3HPbyn/wrgp4zOMvzKnQrzvzGNPEYzD4mMKkj9UrRvNhVieSP6U4KVGDUVhnyF/3Rz+FTjODX61h3ekmz6iBAhOWH6V8Vf8ABUi4QeI/DCswGLS95I9TGP6V9rKRuds18Sf8FSdreJvC+SOba75P1Svk+N3bJpHn5r/ukkeafsOfGPwJ8FviBrHibxpqv2K0n0dYUk+zySlpA4IACZPQAivqq0/4KMfsyovz+PnPH8WmXI/9kr4f+C3wR8efHLVr/wAPeBTbmeztknnNzcmMbGbaMdcnj8K7hv8Agmt+0msxjTTtKZR0K6tgfqtfA8N5pntHAqOHpc0OjPHw1fG0qCVOF0fVy/8ABRz9mEna3jxyfbS7k/8AslTL/wAFD/2bJos2XjiZyRwq6VcE/qBXyY3/AATa/aUSPJ0zTeD/ANBgD/2WuY+K37Lfxi+CvhuDXPGmkwpaSTCJpLS783Y2Mgt0xXvVs+4ko03KVOyQTzHNIK7hZeh9XeOv+CmHws0WyJ8M6Bq2qzHGxVgWFD9SxzivlP49ftO/ET9oXUUfXSlnpkDM1lp9uSY4TgDzHY/eb37Y4rmfhx4Wt/iH4wsvBd3rUWntezeVHdXA+VWycA89+1fbnwJ/4J7/AAm8EXdv4k8WXU3iHUIsNGt4oW3jYYP+rHDfj9a87B4vPOJG4LbqTSqYvMdG9Dxz9ir9izU/Ges2XxQ+Ilk8OkWsiy6dazJta9kU5VmB/wCWXPB74r7w0+1SzjWJU2hOOO3SnWOm2VhbLbWUapGq4RQANoHRR6D2qxsJjPH0r9GyTJaOU0LLWT3PoMLhYYenaO48HIzUMJO+QZ/WplBwOKhKhWYjjJr6BKx3Q8yJUVhyO9RajqFvp2nS3ssqqkaEl2PC8dT7VPAQa8O/br+LE3w3+CV/Dp96sV9rTrp9moIGzeMyuB3AQfhmvLzXFfVMFKpfozDE1oUqUpdj4k/aa+KCfGH41an4hW4drQ3v2S0+YkLbxFVDfQk7s+hr7Y/YI+FDfDz4N2uoX1qY7/WpmvbkMPmUMV8tfoFwa+F/2fvAw+I3xd0nwrKq+TPeLJKGI+WFCWfqem1VHvX6i+HLvTNL02C1hmhRIo1EaeYo2gAADr0wBX5tw1ThXzCeMrPRngZZGNSu60joI2QkBRz3p7ZIxjjvWemu6WM5u48+0g/xpy+IdM6C4U49HH+Nfpqx+D5fiPf9rT7nhH/BQL4YyfED4KT6/pttvvNBuftttgDPlj5ZB/n0r48/ZY+Ki/CD42aTrV1ctHZTzfYr9xnHky4AY/7rbf19a/SPxW2k6/4eutJuyjx3MDpKpYHKtkY/XNfld8WPCN34K8a6v4dnBQ2N7NCBkE7cjByO+3kfSvzLieMMNmVPGUn9x8/mKjSxMK0T9ZdNukvLNJV6MvOD7VZgwi43ZHavFP2Gvi4/xa+COm3d/db9R04fYdSyefNjwAx93Ta1e1bAq/L05xX6TlGMhi8JGa6n0OHn7Wkmuo7IPQ1HuAOSafbAFOfWlr1W7GyVjy/9rJif2evFoJ6aDPg/gK/M3R7uNNUtzIM5uYun++tfpj+1ugH7Pni7H/QEn4P0WvzF0ZC2pW6gf8vMf/oa1+P8ZP8A4VaL/rc+Wzh/7XT/AK6n69+GSRpVsCf4V6/7orRXJL59az/DakaXbHHGxT/46BV9QQXI/Wv1HLbPAxPpaPwCjBIBrI8ZsE0S7fHPlf0NawOeaxPG+T4cuwO6AZ/A1nmbaws/QVS3sz8idUmADkHPD4x9Wr9Vv2al3fA3wo/r4bsf/RC1+T1+XVCCc/I3T8a/WX9miBo/gN4RQ9f+EasMg/8AXBa/OOCU3jqq8/1Pn8oTdabO1MYYc/rXn/x/+DOj/GL4f33hbUoUC3ClrW4IG6OX+E+3PHFejGPaBkU2WFZICpXPHSv07HYSljaDpSR71Wkq0GpH48+P/DnjH4J/EG50rVPO0/U9JvNyTRkqVcZKTKR1PGePWv0N/Yq/ajtvj/4KW11edINe0xUg1e2AxuOcLOueok7jsRXOft6fssw/FnwZN4t8O6Yq69pEO6AoAWu4cfNGfVuSQewr4n+BnxZ8Q/Ar4l2Xi3Ri/m2crx3luxIE8O5vMjbPf09CK/Koe34azZp/w5M+ejUq5biuX7LP1yKSsfb0zVXVkd7GUOMnPOaxfhL8SdB+KXg2x8ZeHL/z7a8tw8ZU5KHAzGf9oHNbuog/YZATk56mv02Valisvc4bWufQymqlLmR+RXxVh2/EXWge+s3vH/bw9fpF+xCc/syeDlHbRYz/AOPGvzj+K6MPiTrSEdNdvc/9/wBq/Rv9h0s37Mfg0k/8wWL/ANCavzLg2Ns2rPz/AFPAyh3xU/U9djJzgVNUCZ3cVOBngV+wRPpyhq6Z0+fHdG4/Cvye/abdo/2iPF6Dj/ioJ/5iv1j1PabOZQf4Wr8of2pIyP2jfF4AxjXZD+q1+Y8f3+rQfmfO5+rUF6lXwr8B/jf4z0NfEvhb4falqOm3JdLe5giV1YqQrYyc8EVctv2af2gT+6/4VHr2Rxj+zWr7l/4J46fby/s1aK80QJ+13xBI6f6Sw/pXvEem2ecC3UfhXPlPCVLFYOnUjJrmSM8NlMJ0YyvuflT/AMMxftCkY/4VNr3H/Tg1Ml/Zj/aHVMN8JfEOMZyLA1+rLafbE4EC4PfFC6bagbWiX6gV3T4DpSb95mv9jUm92fkvc/s6/tAQqWb4VeIhj/qHPX0f/wAE2fgz8W/B/izWPE3jjw3qOm2UmnpbQxX0RSSWUy7t20noFOM4r7VfT7VlwqfiKfBZxQ/6vjjua3y3gyGCxSqqbVjbC5dHD1uZNioAMgU+P/VhRUZAV2A7U5PQHtX3tKHLTse2WFG7vUkOcHPrUEXZadDjccVsA9lzyKj2/wC0fzp5VtuM0mxvSgBLZvLL8ZpU+8KZ5ntT0+8KAHDnnFLQBgYoByM0AGB6Cm7vm9qdUdABkjoabGTu606igByMTwadTVZRxSqcjNAC0YGc0UUABAIwagkf92Tip+lQMCYsCga3K1APcGnY3o6gVC0TZyDXPAsnDTY4NPseVc+9RqfNbLVNbAKu2toWRmSUUUVRmV45WHBFNhbJlJOPxp5B9P0pphJOQKTWgDbckhz6Cn2mCh9RTbcY35GPSnWY+/jsK5obmtPRkoyGwKkiwMgCmKAXx71J+76d/rXTAzluRoO9OpE/1TUpzTJp7BRRQCQcig1CgEg5FBJJyaB164oAczAr9abTmLL3ptABRRRQJ7DbcndIKmqC3OXkI9ad/F978KDOAtKvUfWliGBtFNoNQopE6UtBmFFFFACKRjrSGQFcUIeuTSsQBzQOGqPE/wBvIB/2YvEYI6RQf+j0r4W/Z42xfG/wsdv3vEVrwPXzF/z+FfdX7d+G/Zj8SYx/q7fH/f8ASvhL9nqQn46+E1z/AMzHZf8Ao3/61fj3FVln1H1X5nzWPVsfB+n5n6q6f/q1NTg5JUiq2mMPKA9quIO9fqmB1w6PoVzWIjndx60lSHGSQKPIHdq7nboNXI6KcIwejinUihi5zwaSpKagUjI9aAsylM6xISwGMZFfnn/wUC+Mi+Nvjc/g/TbndZeHIDagKfla6kwZD+Awv519s/H74k2Pwj+Fus+Or2X/AI8rMtDEzfflxsQfixz+FflQ8ms+NPE5ly09/f3pffnJknlb3/2iPyr8341xy9nHDQe58/muKatSW7Zo2Nj4gaP7dpdheMjEhJbaGTaegOGUU+d/G8S4Kat9S1zX6Zfs3fBiz+Fvwz0vwksOZLSyRJTn70hwznPuxPNehjRbYLj7Ov0L/wD1q8rLuDK9XDKoqjV+hNPKJygnztXPyBW68diQlLjWBzxtkuaswXfxKdQq3+tDPcSXFfrkdIscZ+zpz60q6Vacf6Mv1AH+FeiuCcUv+XrB5NUf22fkkF+JW4yyXOsMO433PNZer2mu2wN9qlndLuYBprhJPmPpubvX6/nSLGXjyUPuQP8ACvK/2rfgtYfFL4Maz4W/s1RP5DT2snlqCsyKCuCBznBrzsfwVVVCU3UbsRUyWUYNud7HyP8A8E2/jWfB3xhfwDeTtHaeIU8uEc4FzGC0Z+rJlfwr9FLOfdHvReCK/G/Q9W1fwT4ysdd012gv9OukuImB5WeJun1JUr9DX61/CPxxp3xF8CaX4z0eUfZtSsYriIA5278EqfcEMp9K9TgnHSTlhZvWJ1ZNiG06TeqOtBB6GikMG4bgfemgE9BX6Se49xKKKKCyEsQeDUkeccmon+8aljz5K56b6AFKgjgV82/8FIPAf/CQ/CdPFUNuXk0S8E7sFzthcbHPH4GvpEt8/Jx81Yfj/wAI6f4z8KXnhjV4g0F5bvBICMnY6gZ+vOa8LOsJ9dy6cEcuJpKtScfI/Lv4C/EOX4W/GXRPF5mKR6fqcYuyvaFsxyf+OuDX6q6LqdpqGnJcWUqvHJGGRlOQVOMfpivya+Lnw/1X4RePNS8F6vavHLYTPGzMpAlXkRvnvlP1FfZP/BPv9pWLxn4ZHws8V6js1LQkCW3mPlry2yQpPOSynr6AV+e8HZh/Z2Olg6ztd6HhZXXjh6roydtT6toqGN1devI681YRQUBIr9di1JXPpNBq4XoKQxqTkgZ9aUDJxTwijtVCIwijoopykjAB70NGoBYigKARhcUAeI/t4Af8M2+JlY9beIdf+m6V8N/skqIv2k/COP8AoOgf+QpK+4v28Jo4/wBnLxCHIG6OFefeYYr4e/ZSyv7SnhA54PiBOn/XOSvyPiO3+sFH+up81jV/t8T9SLMEW6hV/hH8qnX7r1FZ5MKD0Wnx7gGHPNfp2F1w6PpKZCzYdx7V8Q/8FSpCfFnhaPjmzvD+sYr7ckJLOCK+Hf8AgqOWbxt4WX/qH3mP++0r5Xjh3yOX9dTgzPTCu5T/AOCXKq/xO8SRZyzaLFgk/wDTY195wW6kDcvavgr/AIJaHb8W9fQ99BjP/kavvqNguA3THeufgSlGeVRuTlTbwyGtbQElWAwPauT+Kfw00n4heE7/AMK6vaJJbXkJjGQPlJGN31BrrnKkkKMikGXUxEfTNfYYnB0MTRlTtud9SiqsbM/I34y+AvEvwR+Jl74Q1yF4prKXfb3CgqssefkkU9yMCvuv9hr9paL42eBjoGv3ITxDocaxXwI5uITxHOPUnGG9MVF+3v8As4QfF74dSeLPDenBte0KJ5bRgvzTxAfvIcdyRkj6V8LfBP4reJvgr4+tPGuhTOJrSU+fBuOJoTnzIz7nkD0Ir8sTr8MZwmvglufPJSy/E2+yz9coWVkwMHjnFTIMsOK4z4PfE3w78V/BWn+L/Dl4JLS+tg8exsmMngofVlNdnCflGcZxjiv1jB4mliqMasOp9BCSkuZbDxjHAxUcvCE4/OpKbIAVwa6nsbrYpSzLb27PIegzzX5w/wDBQP41S+P/AI5SeFLC9J0/w9EbRFDfK1y5DSt+AwnsQa+4f2j/AInWPwp+FWs+MbiYb7a2doFJ+9I3yxr9Cefwr8r1tNX8a+Jo9oabUL67xuJz5k0rg5PsWI/IivzjjLHvljhIPWR85nOIlK1GPUn0rSdZKC/s7O8ZCDslt4pMdgcMn61dc+LYEAV9VHHHz3Ffpx+z38FNI+Ffw30jwbb2y5srBY5W2glpDhnbnrliea71fD2meXgWqccY2Lx+nWvPwPBlerh4zjUav0MqWUVHBe+0fkNHc+Mi5Cyaqfo09WoD49kUKP7X57jz6/W7+wdOBytqPrsX/CnJo1mowlqP++VH9K6HwRi761WbLJ59ah+SPk+OoMkpqzKoxgi4wayL+HW7eVry/tbhA7jc80b4J47sOtfsMNLsmYxvaD3JVT/SvKv2tPgnZfFX4Laz4dt7GFbqOI3FlKkKhhKgyvI9fSuTH8G1qeFlL2jdjGtk0lBy572Pk/8A4Jn/ABnj8IfF1/h7qk+yz8RRYtwXOBdRgsh+roSv/ARX6FLKsiZAr8dND1fV/Bniyz1zS5Xtr7TrlLiFwcFJYyTg++Rtr9Y/g14/0/4l/D3RvHOlMpg1OxiuVAOdhYDcp9wwYY7V6HBOYTcHhqm8WdeTYhum6Ut0dbEAq9RTykeOGH51GmwcE8+9PAXoMV+kppnvHln7W4Zv2evFyr20O45+gFfmHoMmNUgUnkzx/wDoaV+oH7WpDfs++LlXvoVz/wCg1+XHh851y1QHn7RF/wChpX49xgv+FSj6/qfK5ur4mn/XU/YXwzhdIt1/6ZgfoKvbsseKoeHM/wBlwc9h/Kr2DuJHpX6lluuCR9JQ+AQZwQB0PFY3jliugXIx/B/Q1sev++KxvHSn/hH7r/rmeT/umpzXTAz9Cp6QPx8viQjkt/A39a/Wz9nCXd8EvCRH/Qt2H/oha/JLUMrA+f7jcj8a/Wn9m5SPgf4TUnp4bsAf+/C1+dcEa46pY+eyd2rzR3wZfWo2J3BQelJEWZMZ70pTc1frC0Z9KVNRtUuUaNh1GOe1fnv/AMFAv2W7n4ceLpfip4Q0/Gh6q+b1I04tLnB5AA6N/Wv0PcguVPY81g+N/BGh+OPD954Z8QadHPaXUZjkjlAO9SBkg9j6V8zxFk9LM8O1b3uh5+Nwir0mup8AfsHftWTfCLxjJ4G8T3rHQdQnAnaVuLGY4/e/7pyQQOlfoi99b3+mLc2zK6Sxoysp4IIzxX5fftRfs7ax+z149+xQxyNpV5ul0y5IOCnIMZ9XAr6K/YS/arfW9PT4J+ONQze24H9jXM0nM8QJ/dEnq45PPYV8fk2aVcu5sBiH6Hk4LFyot0auh8o/FpWHxW19R2169x/3+Nfo1+w+oH7NHg4D/oCR/wDoTV+b3xKmNx8SNZuGIxJrl4eD1H2hv8K/Sb9iZBH+zN4NUDj+x0Gf+BMa5+DmpZtVS7/qTlGuJn6nrVqAytkDrSMMDj8aavABpckjk1+u2R9QUr4EwTADsa/Kz9qJMftG+MM/9ByTH/jtfqpeH9zLj+6a/LP9qmHy/wBovxaf72tMf0WvzXjxXwkPU8DPdaKXmfcP/BPHB/Zq0Uf9PF5/6UvXvEYBLKewrwf/AIJ3MD+zNooOOLq9H5XUle7hicnGK+r4da/sqn6I9LA3WFixKG6H6VIDkZFQk4Mp9MV9AdTVh0S7kAI4qNlBGAafBKO9MZvftQEdyOHO2XHpTrc46+lNtgAZPfFSqQDk0Fj6Lc4kY0UqkA5NAD6DwM0U2I4efnv/AEoMyIgjrT6KKDQcWAHy0KQOrU2nq2eDQAnme1Np+X9BTDxxQAURRbjyaKKAAjHBpyHn600DJxRQBJTWYhuKA/qKaST1oAUsT1NJS4PoaYS/YUnsA1sgGq8ihm5qwc44phQ4yRXJACG1UhQKmjHPHao0Hz5FSW2F6muqAE9FFFUZhTIBxT6KT2Art0I9zRYnDsB3NDHIJqK06t9TWFDqaGjUdRgH7OOfxqTIPQ10AFFFFAAMd6XJ9TSUq9R9aAEop21/7360hGO9ACUUEknJooAKaPuH606mMD5mcdqAEgTZyBTosEEDtRCDhifWm24EcTjPeppgSUq9R9aNrHtQFbI4qgEooooMwpN6+tOX8PxoyByFj/OgCKAdMU50zk57UikA80hkIB57d6T2JhoeI/t8Obf9mrxBuPB+yD/yYSvgz9nucH47+FlBGf8AhIrPH/f6vuz/AIKECaf9l/X44Fy261JI54E6En9K/Obw74i1XwN4qsvFeivGtzZXyTw/aF3oJUYFSRkZB9K/GuMJeyzalN7I+YzSpyYyL7H7EacUWEHeQewzVnzFzkSkn3r824P+CmH7R0KBGh8O8eumyH/2rUq/8FNP2jgQNvhvnof7JkP/ALVr3sLxrg6NFR1+47451QXRn6OgkD5pKUSxnjdzX5yD/gpl+0ayYK+Hsj00qQf+1aif/gpz+0UmPk0A/wDcLf8A+OV0LjrArq/uKec4bzP0f84AcSD9KQOWGPM/Wvzcm/4Kf/tHYKqfD647jSWP/tStDwv/AMFSfjnpeqQz+ItG0TU7NNrXEMFs8MhQlc7SGIzzW1DjXAVaignv5BDOMPKXKr6n6Lxq+0MX7dzTWYgbgePWq2g6smq6fDfIhCywxuik9Ayq3+NGpXqW2myTyMFAjOT6cZJ/DH6V9bKvB4b2qPX5lGN0fFf/AAVT+Ls0A0f4QabMGyTqOoor/NsB2QqfqctXkn/BP34af8LG+OVhqN7bmWz0SE6hO23ILglYh+Jyce1cB+0b8R3+MPxp17xk0x8u6vXWy5OEhjPloB7fKSfrX2X/AMEwvhcPCvwim8eX1qyXHiG5Mke9MHyEOyL88E++a/JqcZ5vxDzS+GL/ACPlIXxeZXeyPqfS4mitRGOw4qwQ/I5plqpRAu38Kmx/Fiv17Cx5KKR9VD4SExDOaQqRUjYK7vzpjfxfhXQUNhHeoLuBLi2aKQZVlIqW2kZic9ulNyQMDHXvXNWpOpRsJxurH5Xftn/C64+Ff7QOsaXaxGO1vpRf6d6COQ5P4hxX1F/wS4+LsfiDwLf/AAxvrj/SNDuTPZq5/wCXWYk4/wCAyBvpurO/4Kn/AAvbVPBWkfFSxh/e6RevaXzYGRBL0PTs4/WvmH9kX4v3Pwb/AGgdF8QzSslpPcJp2pxhv+WM7eWSR6h9jD6GvyFRq5NxLzL4ZP8AM+Wpp4XM7dGz9ZraRWGc/SlT+P61X0yQy2yv3xzirDMQmT3PNfruGk50bn1qQlFFFdK2GReSc04wjsafRTAgIOcgGkIynLYwOM1PtHYD8qYVyc7f0rC19yNT5o/by/ZiuPil4SHjzwfpvma7pUR/0eNPmu7cclBxy4PINfCPhTxl4j+HvieHxBpF/NZajZXJeN0yGikGeGBxn0KnrX6/zxLNGYyBg9D6e9fK/wC13+wVafEyeXx38KYLax1oITdW7ELHfnHb+4+T1796/O+JOHakqv1vDaSXY8DM8A5P2tLc3/2WP25vB/xWtoPCPi67h0zXkTatvK2I7rH8cbE4yT/ATxX0PBeQ3K+ZBOW45APSvx88aeCPHnwz1n+xPFWg3ml30JysNwrKXIPDK3RvYg16T8Hf2/vjl8Jli0p9Vi1nT4lOLHVwzPGPaYfMPoc1yZXxZXwq9jjU9Oplhc2lTXs6+jXU/UBJHDAgEjPpU4cnA3da+NfBv/BWHwZeWqnxV8NdVtp2B3fYbyOdPw3FTXRSf8FT/hFFEfs/hLxE7gcKbeAfqZK+rp8X5Q43c0eoszwkldzR9RrI6gsznr3rnfiB8T/Bvw00CfXfGOuwWdrASzy3EmBnP3QM5btgCvkDx/8A8FTPEl/bSW3w/wDAkFju4S61W581h2+4mB+Zr568Z/ED4u/H/wAXQpruqalq2ozPiztIIshcnjZEOEHYt+teRjeMqUlyYROUmcdfN6aVqWrPSf2tP2y/EXxzvR4Q8HQy6f4YEmXR0xNqLKRhn/uRjgqvXPWuO/ZRkVf2g/B878f8T6LknvtYf1r2r4If8E69Zn0tPE3xfkNu4hcwaNA4aQkp8pmk6cHBAHpXnn7LvwI+KFz8ftFEnhzU7ZNL1dLm+vLuyaKKNYmOQWY/MSMAEetfJvA5riMzpYivF6v8DzIUsbWxEas1uz9JdPyYFOOwp56nOabYL+4GQanVQcrj9K/ZsLHlopH19NWiQFTtIx1zXw3/AMFSVx448JkHGbG8B/77SvuYgeWTXwv/AMFTSB438KEkf8ed73/2kr5HjXXJZI8zNrvCMq/8EvYdvxT1uXH/ADAIxz/13r7wLdm9K+D/APgl7LDL8T9bjRwf+JHD0I/5+Ca+8QmcnPHas+BPdyqKDJ/93QhdaIpQGOfXrTUXczD0pipg5Jr7o9YW5hiuI2gJBDZ61+dX7fX7O0vwl8eTeOPDtjs0PW5mkyiYW1ujnK4HZuor9FQQ33hxXHfG34T6D8YvAWo+DNetw0F3AUSTgtFJj5ZFz0I/lXy/EeTxzDCc0V7yODHYdV6bS3Phb9gD9qY/Cjxkfh54svnj0PVLzEUsz8WNy2ffo549q/Ryxu4rqFJYzwVBznNfkR8UfhV4h+Dfi+78G+IYSs9rI375WIWZOSsgPc49Olfc3/BPD49aj8T/AIcN4S8R3Tz6j4dkS3ad85ntnG6GQk9W4Kk+1fMcJ5licPXlgq/TY8zLMROFT2Mz6XyGJyO9Nc7IyNwyDTVlLDcOprP8S6tBpWizandNtWOCSSYk/wAKgkn8hX6HXrexoOZ70naLZ8Zf8FRvi0De6X8KNLn3fN9vv41Y5HOyJfoeW/CvM/8Agnt8MJPiH8cbLWr6182y8Pwfbp2xwZRlIR+eW/CvKvjh8Trj4wfFPV/G80+V1K6aW0y3CQKdkY9gFGT7mvub/gmz8MG8FfBo+ML61KXXiG4N2Qy4b7OnyRD8eW/GvyPDRqZxxE5z+GLPl6cXisx5nsj6W0+Hyogh7Dg1PgYZt38VEfyLgDtRE+YGJH8XcV+wYaPs6fKfUqOhGka/OW9eKQIpOMVKThSKiz82PaugVrD4YwshJIwPeoryBbm2khYYVgetOwq/MaUfMuR+VYV6Sq02hNXR+Vn7anw0l+F3x51jTLO38u0vXF7ZHGAscpJI+ocEfjX0l/wSp+M413wjq/wk1a7JuNFuftunI55FnOfmUD/ZmDfQOKX/AIKh/C+LWfCGnfE60izJpV41rdOo6W83Q/g4z7V8qfsr/FbUPgn8e/D/AI2CubeW+TTdTgVj81tcMI2yPUMFcfSvx21XJuJfd+GT/M+Xg3g8z8mfrdC2VDEYpF+4On41Dp83mwAscnHJqc7QMMcCv2GjNyppn1cXdHmP7WC+Z8AvFintoNyf0xX5d6MFi1+13DpcRHj/AH0r9Rf2qRv+Avi2PHH/AAjtzg5HPHX+f5V+WVhcKNagO4D/AEmHjP8AtpX5Pxen/alDTr+p8zmy/wBqp/11P2J8PADS7cY/un9K0QMlvpVDw4R/ZNugIz5aH9BWhkgviv1LLdMIj6OkrQGx4BPTk1heOyBoN4+fuxE4P+6a11wrbs96wfiPKE8I6q7fw2UjZJ9I2NY5lrgpLyKq6QZ+QGpki2fJHMTH+dfrZ+zudvwY8Lrn7ugWH/opa/Ie/wBQhe1RRKp3WwI2kc/LX67/ALPg2fBzw2pPI0Cx/wDRa1+d8EwnDH1Lo+cylP6xK53UBXyzlqkVIyMg8/WoYSNnFPDEd6/WD6YjMeCXPU9aZIoIx/kVOWJ61EyE8YoA8v8A2j/gbpHx0+Ht74cuY1F3lpdOnIBNvcDvnHQ45r80L608XfDLx7caTqKS2Wq6VdkOyMUMbqThge+R/Ov17ijjaNg6jPOM18hf8FGf2arrWbKX4w+C9L33thFt1SONPmngP8YHdl7n0Ffm/F+SOrS+s0V7yPnM5wDqU/aQ3PjPUL251W/bUb1h5ryFmEfQsTuJP45ya/UD9jBAn7NPg4Z5/sWE/nk1+VkGpxsyHeCCODnqAK/VD9i6bP7OHhGJxyNDtyQfpXz/AIfUqsMVN1Nzk4fjKNSXMeqUfWimbiOAa/aD64rahkW0pA6qa/LX9rB8ftHeLFGP+Qzgf98rX6lalzaSE/3T/Kvyv/a0dov2ivFjMvI1cHJ/65qa/N+PE1hI27nz2e/w0fbv/BOe4A/Zs0hWb/l/v8ZP/T09e9o6tMzBv1r8v/hB+258XPg/4Sg8F+E4NFNlaSyNH9ttGeTdI+85KuO5NdQn/BTn9oMOWWDw2OTj/iWzH/2tXPlHFmAweBhSle6S6GeDzfD0sPGDvdH6Ms55IcYFNV8ZDN196/O1f+CnP7QY+9b+HDn006Uf+1aguv8Agp7+0OoJjtPDgx/04S//AB2vRfG+Xr+b7jqed4ZLqfowDCTgMwPsaXAPO4/UmvzWk/4Ke/tJZ+U+Hx/3DHP/ALUoX/gqH+0vGfueHW/7hUn9JKiPHGXt/a+4j+3sN5n6VI2RsXGe+KRhkV81/sG/tieIP2j7bVNC8bWEEGpaVFDN5trlY5opCVDBWYlGDKwx0719LxgMgOO1fW5fj4ZhQ9pA9bD144impxGknaFUU/TpvkYOenc1G0OSW3mo1yq4Jr1Kex0t3JvtGOC1MWUp1PWolJLZqe39hTESUAZOBRQCQcigA6UAkHIpy/N96m0AOVuyrTacqgr9abQAUUHOeaOtAACQciiikQHGMd6AFpVBJ4pKWP8Ad8YzmgB4AAwKQjjAoDA9DS0nsBHUcvepe/49aa/3TXJACpT4+ccd6Wi0/wBYTiutbAWKKKKZmFFFI3b60AUmzzg/rSRdeD1NPpYxhwQO/NYX1udNN6luooDyRUgORk0tbmQUhdRTKbHktjnFADqfGcDPvR5aeppaAHLgLupMnOaX/lnTaACiiigAooooAKIunTvSJ0/GnKeRzQA+pKi3LnGaCNwwDQZjWxnikpSMd80lABULMpHrUrHAzmqrZzzQaEm5j3pjPhNxNIn3hTlQ7TQBznxC+Hnh74oeEL3wb4jhlls76PZLHnaR0IIPrkcV8+yf8EsvhTOpI8X68nPyr9ojO325Svqe3t2IGFPtSojBmBU4+leLjcnwWYT56kLnHUwmHxD5qiPliP8A4JX/AAmjXa/jHXiT38+L/wCIpy/8EsvhLnnxbr5x/wBPMX/xFfU21tvfp6UR4zkZz34rg/1Vyr+QzWW4TpE+Wf8Ah1l8JiGC+LNe57m6j4/8cqP/AIdX/ChsK3izXen/AD3iP/slfViRyBCF7+9K9uQuc546Uv8AVPKnvAn+zcL/ACnyc/8AwSq+FTfP/wAJlrg5ycvF/wDE1N4a/wCCYHwm0fWrfUp/E2tXlvHMrzW0wj8ubBUgHAzgkDp6V9TrG/QqaRraTcCnAHvV0uF8qpS5o0x08vwkZX5SppuyygW3VcBFCqB2AGAKW/iTUbCSzeP5ZIyjDOOCCD+hq20CYySKIbZgWJ/CvdjhqfsfZLY7uWNrHx/qn/BLDwZP4xbVrHx1e2+lyz7vsElruIQnLIG9Dk19UeD/AAvpPg/w7aeGdFsBbWtlBHBbQAfdjQACtcRnGM9O2elPgQbSQcnpXnYPKMHhKzqQjqznhhMPSblFasdGc5bPU06kiAWLFDNjtXtm8AJwM4quWAkJzUtQfx/jSexoKj+UhULmmGQgfLn2qUwgdMmkEHPb8qOgHO+Pvh/onxK8IX3g7XrbzrK9haKVScZU4OR/tA8j0r54+Hf/AATJ+HHhLx3beK9Y8TX+q2VncrNbadNAEUMpBQSN/EFIH4ivquOAhsYIH1pJImKnjnFeNXynB4ysqso6o5JYKjVlzvdCaeBFCsQ9P8KsLjJwe/Woo02qCO1Oicktn+90r1qMVGnymr2JwMqCRUTY80/WpUOUB9qqsDv3c/WtC4MnoqCPL7wc9O9LB94fSgslZdwptsPmkNP+tNthktjvQAzaMbc1HJAjRGJ1BXuDUtLsBXdWMoxe4mrnF/ED4O/D74o6Q2keNPC1pqFu3AS6g5T/AHWxkH6Gvnzx5/wSv+FOtSNceC9c1TRyVO2HeLiEe3PP619YYIWTAPSnBsjDIcfSvGxmQYDF6uCuclbBUK/xxR+f2vf8EtPibps7Dw14y0i6QH5VuoZIj+gPNQab/wAExPjbdSJb6lrmgwx/89FnnkI/DyxX6DhI2ONp/KniNQMV474Iy2bu0cLybCJ3R8c+Bv8Agltp8Esc3jrx1cToo+aHTLURZ56F3JOPwr6E+EP7Nvwr+DkMn/CEeD0glbia5cCSdifWQnOPYcV6EM7Rt69qF+UEkZx6jpXq4HhrLcvfNCGp10cDhaPwoasMKIFYDAGMUyPTtPiJljjQMeeKnIzwv603y29R+dex9XpSd2tjrVNIlhK7QpPapCwAIBxxVVchsU7cMZzXS1pY0HuSRj868l/aI/Zg8H/tA6Yll4kkltbmzbdZ6haENLDuxux6g45FerJIXXIHShRtXI7c1w4rBUsbQdGtG8TGrRhVjaWx45+zD+yN4V/ZxW9u9I1mfUry/CLJd3sSqyIuCEG3GVyc17KiHZjJPHUnrTYhu3D8s1JF93pSweDoYCioUo6Co0YUo2iRxj5pCR24o8z2pSAQfeoyWzwK9A3F6UjKHG00m8+gp6ruXINQ/eVgPKPj9+yn8Pfj/pqJ4hgkt7q3GLTULdQXizgH/e71D+zd+zL4T/Zz0a5sNEvpb28v5la9vZk2GQLjYgHTaBn6E162sRXhRjHvTEiDMQRXkLKcLDFe35dTmjhacanO1qPtpFbEeOfWqXiHS4dZ0yXTbo7o5oZIpFHdGGD+hNW4lCkilRMNwO9ejOnCvQ5ZG/LpY+Obb/glX4NtfFg1M+Ob7+ymnDjTjDyseQfL3enJB+tfW/hnQ9L8M6RBpem2ggtrWJYbaFBwkagKqj2xV7yd4YsvQ8e1O+ZVGAeOntXm4LKMJg6jqQWrOWGFpU53iTxklcsaXd822kgyUAPXvSqOSfevZlsdURahCkTE5qakYZGMUk7FFQsGJ+bPNIZCpyppUi+eQY9cUgUAYqwOc+IfgPQ/iT4Tv/B3iGyaSyvImhnTvhsfMPcHJHpXz34G/wCCZvw78OePrTxLqnjC91OzsrlJrfTpLYKu5MFQ7Drg9fevqiBXRmJGMnj2oGViYZ+leNicowGLxPtpL3kcUsHh68lKS1QtovkqI1BxjoTUzMFFNUFgMj05oK4JA4xXoQpuCsdiVkYnjLwlpnjzwteeE9X3Pa6hbSW10qtg7G4I+vpXzT4K/wCCYfgLw94sttZ1Lxdd3+m2N2skNjJZbSwVgyq7Z+YA9T7V9WlRuxjGe9KbX1I+ma8/FZVhcdVjUlG7Rz1cJRrNSnuhtlCsMKoqgAY4B6cdKn3jedp4NQquYzjsadCpIOAcfSvSpUlSpcqN4w5EP8tW5BxVHWdOh1Kzmsp496TRlJFHOQRgj8jWgAQPmz+VRrjMhPHFKdJVIWkEldWZ8b+IP+CUnhLVfGr6lo3xAurTRCysdMNjvaMbsmMN6c19ceFNBs/D+g22i2KbIbS0jhiXPIVAAP0q9bK+07D1XrnvSx2qH5fMA5zjNcGEyvD4Oq6kFuYUcNTozdizgA4FFFFeudIUUUDMYBB6mgCFTsJYDvVPVdNtdY0+SwvoAysCrK4yGB7H1yKvNG+flNLGMxHArCpRhXpckiXFSVmfInj3/glp4F8TePJPE+leNL3SLCecSXelQWysOoyFfsCCeBX0/wCAvCemeBfC9l4W0gCK2s4IYIELZ2oi4AJ78YrURSgK56VOsYCZx27152CyrC4So5wVmzGjh6NKV4ocJMjkUeavofyptScdf3devdHQV8LPE0ci8HrXgXxe/wCCf3wl+Lni6bxpfX2q2F7eMDdvZEKJiMAFg4IBwMcelfQKx4Bx60Iu6MkqfxrzsZgMNj4ctaN0c1bDU8R8aufKb/8ABKP4Qs2+Px14mU+1xB/WOnL/AMEq/hQsYT/hNPEROOC08H/xqvqsBivHTp1p/Kr+FeV/qtlX/Ps51l2DX2T5Mb/glb8LhwvjPxBx63Fv/wDGqb/w6o+E7cSeLvEB/wC3qD/41X1fIkrMRjjNPjVgMN2rN8KZW38Af2dhm7cqPlBP+CUfwfAw3ibxCf8At8h/+NU2X/glT8GirRL4l8SKx43C8iOPf/V19aEA8VEUJJJBpx4VyqL0gL+y8L/KjyX9nf8AZQ+Gn7OcF1N4Ktrt7m/MUd7c3s/mSMkY+VeMAKCSePWvXYCHJOevvUJTcRwfyqSIbeox6DFe3hMNSwVPkpx0OunRjSjaOxPCwBcA9D1qAxgrwP0pUYDPNO3DGa7zcggUAOe1WFPQ1HT4zgZ96AF69TS5PqaSgAnpQA5TnolCp3IoX7v3aSE8UAKydwKAoA+ahn7A02gB3l+9Np3me1Hme1ADcnGM0EknJoJyc0UARWhIQKTwOtJaHl+vSpSF6kVFbj5pTQBYi2iIZ7mkDEdKTpRQApYkYxTWyATmnWxJPPtTGIJPpk0tAG1HZnEh571GevFTWxBEmfbFMCaiiigzCmuT0p1Iw3DFRHcFuVo4u+T9KfZgZcD8KSmxExngGsjZ6bFiL7lMsxzTKWE/u2FbrYkfTo8beKIh8uB606mAUAkciiigAwTzRT06fjTKACiiigAooooAjKQ/e3NTouJJM049OKZb/eek9gH0VJgegqOueF7gRLFtDkn6UtSEgcmmeZzjd+ldIDBBxkCkIONxqUEnAH40m1T/ABVlrcCrahsZOetSwxFTwD170+GJQNw9alrUBVbaMAUEk9aSigBH+6abH65PXigqE65NOXaTkjvQA9MU6mx96ViAOaDMTYOxpHUD6GnBgehobGOmaCktCJU/vClwMYFIzlei0RfcoKEMQPNCRlTwacWA6mjcMZzTuxWQicZzxSMQWxmhSP73aoBG5YHPf1pEw6llcY4oYDaeKIx8zg0bhjdQWVh0JY9PenwKScmltx/rOO1SoAo6dqAAKF6U3yeQA1PpQpPQUAN8sev60BADmlooAKcWOOVpASOhpq5xzQZiRgqpAppURnBxUgxjgimtLF3IoCFyBm5yPWniNgMib8qIDwPrSkAnNBoNiyCD6U+L7pIoVSBjH6VHFKoyD+tAD4SB5mTT0POKj53ZwetPU8g4P5UAPpvljPWnUUGZAkTeZhjxn1oikAVu9Sp1/CofKMeQB1603uTHYb5kmcqTTxNOMZ/lURGDinRNtJ+lI2JTKAOR29KZCc8e1MAJ6Cl2HruoAfuOc0qsSeTUWT6mkoAsD1zSpgKRmmRD5RxRE7Dg0ASmUdh+lRpnbUoIIzUQZT0NBmMp4C7eDiglcdqjzjj0FBoPIQDrTNozupnnEdVp+9fWgBNsfXqfrT7ddwIIqKp7PGGzQBKkXy5DY9aTyxn/AOvSW5w0hxjinE55NBGjY0/KOn60kP3cClJyDTIOCcmgslSHEP0qMjBwakBI6GigCIqMYFR+UxPNS0UAMEYCY9qWFMdBToQOBSzZxxSsgIqKKKYAAT0pyMTwaYp9/wBaesowCKACBMjDCpDtiXIHenVE65GaCZbCNOM8GmNNu6ntUpwOc/jVRgx4GaAjYfGQ6Oc9BxUlmO9RxQcdTz61LBhfu9KCieo418rg1ICDyKKACiigAnoKACmQdD9adszxk/nSRyCFc9aAGRoMO3Gc0srsq80sQ4z7UyXg8mgBokc9qeCD0qPePQ0kaNnK5+tAlsWE5BFOP3T9KbHnBJFO60DEQYHIpScnNFFBmFR1JUZJHQZoLgSUUUUEBTt+Bk8U2mO+3gjNACZGcZpGYggA1HbKd8hx2p7jgCg0JqROn4023QqshLe9LGcigBJs7D0qTTDwRUcwyvFFjIYmc/kKAJd2BnbQjfw0FP7po2sOhoAdUdFFAC5Oc0lR1LDjyA3vQAlFFFABRS7WHajY3pQAlR1JSEDB4oAZVZeO3erHPbpjimVxrcXQBKCZM46cGn2wGMjuKYsO45C9T2qeFlBmHHHSutbDFoGccikBB6UtMzCiijIzigCFQwP3aEPP1o809M9fao92f4sfhQaE0ZHlYpx4hfiq6lifvVPGcng0APooooAKKME9BRQAUUUUAFFFQSRfv+lAE28ehoTp+NCfdFIn3m+tADqYOvXFPpqqDFk46UAOphGDjNNCAdDn6GgfJ34NACkY4NSUtvKrHBFRMcZJoFdDhKVGccD3puc81FE4IZfyqQLkA0DCE4P41LUKKeg4/CpI84OQevegB1FJuUd6CSRwD9aAGGTJ2kU6IhlyKjCZGc0u7yuc8UAPiGz8RzTqjaYdhmiM7uQKDMdH3qQkbcZ/KosgNjPenEhiQKBx0IzNkYIppfJytRlyueD1pYz5gJU8CgscjBOc5+ppfOB6EUg2kc03dCp3GOsvaa2AkTI4IpIz83BoSUMcAcU5cEcCtRJpijBGQakqKMnaCKit2BZt3b1oGWqKSJv3I96WgCOpI5SBjP50VHQBJSbhnFCnIzTSGz0oAfRUeSOhpysMcmgCKE/NIQOxppOG2mpGYGJselRKDnkfpQA6n25xwaan3qmRQB0oAWqpjPY1JE5YZ560RFWG1jnmktgDzcdjxQs+T0NKVQ9h7YqDocA/SmBNbEjc2eKlDA1DAV8ojPU04IwIJOM96DMlHPNFJHgcAg89qXHGcHHrig0KzAkcUypOlR0ugEsP3aCME9KSM4Xg0yM5D8/rUAJRRkeop8ABaQH04oAkQYUD2paApAHFDdD9K0AaWZeP1pm9D/yyH509sL0WogDnFArISKTd93Ix75pcn1NCRKEwMcihI13YxmgYKcGnKqg8swP1o8r2NEYKCgBNjjkSHNSrgcA00j5sAUrBscDj6UGb0I2kIJz605Lhjxu6UEeo/SoYQDlx0A6ig0L1oQetFQWb4zz27U+CTeTkmktgJKjqQEg5FH1pgR0VCz4OAKN7DgigCaNx0pzMCMA1GjZ4zUZwV65rMCaHHNBcbv8AVJj61Ch7Uw/e5H6UovUB0PQ+meKP4/xoXJIHvUqgBBx3rUCYHIzTMnGKccY6dab3yooAYvMuc03ylz04zTo/vn8aSKQkYY59KAHnpxSQcE0gbLHHT2FJCSpK5oAkPz8pToxgc/rSQkLnHQmgtmMv2oAepwc4pDIoXGf1pgdvLzjt1qKgBwnx94k80GSJhgoaZHGHXJ/Cm7cnbn8qAJ4WOOBSAgxHcajk/dxBk4NLn9yT2x1oAjqW3YKefWogCRkDilBI+bPHrQBbpinDZHOKZCwYYZuaUGP5mDtx15GDQBJ54Pr+FJ5pI5B/Oo1CuNw/nTjGqjJJ6UCbSHRDavXvTfP9qjLEev4VGCD0NAyybgH+Gn1XhQP0GasUAAOR1FMjRl/Olj70pHp3FAEMfH5U+omU7eBSwDBJ9aAJASDkU7evpTajLCKHJPFAnsSCRSRgZ+gpwZD2/SoVjTAfOMjilaJQPmP/AI9WfO7jLS9Bmlpm8Z5cUquD/StCWkOJA60nCikZucqaGbHyigoaCQcimQxZ5z3p/XqacvUfSgAUZG09qFQg5JpwAAwKTHT2oAWkI5HFLTXJHINBmNprf60kCngZOKHPJxSew4bCVHUlR1yFQVxkOAAT61FYHgc9TUdSWR+QD3remMtqMfnSgAdKKK1MwprAg7hTqKT2AiPyjgVA0gzgj8anAyuCKqkMxzisad7mg6OT5hkZp1kwKEe9Ni5PT8aS1GOQK3AvRY8gYopIsiAZNLQAUUDr1xS4G7GaAEooooAKKKOlAEfl4520xZsEjHNS+YOwqs/BJpPYBY5CdxLn25pPtzRAozdB3pkTIAdw6nvXxz/wUp/ae8a+CtQ0v4IfDfVLi01C9hN7qN1bybZJIncpFCrdtx64ry8ZjXhaHMjWnD2jPpbxd+0V8FvAU5s/F/xK0SxmU4MU9wpcfguaXwR+0L8HPiHdGx8EfEnRtQlzhbe1ugHP/AWwTXzp8Fv+CZfhM+GrfV/jRrd9qWt3EQe7hguNkULEKdhY5ZmGcHnk9KtePf8Agl74QuXOrfCjxfe6NqEPMIuZPNjLDp86kMpJP/1q8mnjsfVhdLQ09nRTsz6xju9wznkDnFTmRWi3sV5HU15n+zJ4c+Knhz4U2mkfF6eS71S3uJVjEtwGeKBW2oCwxvyACM89M16Uq4XZnPFe/hak3h3KW9jlnZTsjkfG/wAZfhf8MZoYfHvjrSdKkuBmCO6m8vcM4yPWqNv+098A7tFkg+LfhxwRnI1uD+rV8x/8FPNLi1T4geELKThbmOWJiP7vnR/0JrttJ/4JbfAKVBJdX+tyluQDcx+3fbXzVTMcZPEunTZ106VLkvM9jn/ai/Z/szib4t+HE5/6DcX9GroPAHxL8CfEmznv/AfirS9WhhcJNLpt6swjfHQkHg+1eFn/AIJefs4FGDWOsSfXUQM/kor1D9nz9mr4dfs6aLqGm/D23vIE1O6juLxbm58wlkXAweMDH8q9PBzx05fvNjOpGivhPR9q7R9Oua5bxB8Vvht4X8QQ+F9f8b6NY6jd4FtZ3V8IpZMnA2qTySeldM2WUc8465r8+f8Ago3a6leftLWNpYO3mf8ACPwtAUPIbzHOR7gjPHenmOOlgoJlYeiq0rH6BQTCePIJ6UwLjDbj+Jrx/wDY5+OCfGX4W281/eb9W0rZaaopPzF15jkx33qPzBFexzxkAuV4zmuvL8dHFUObqZVYulUsxomVV3EjjqSawbL4k+DLzxQ/g6z8Waa+qgtv0yK9iFwuAC37sHccfUVzn7SPxjh+BvwtvvFszRtdlVt9Jglb/W3cgxGreqjBdv8AZB9K+MP2RLjXLr9rnw9r+r3ck1zdLcy3E0v3pDLG5LE9ckjP0xXm4rN/ZYlU0awoe0Vz9E0bgbW6fjUWparZ6PYzX+p3KQwRRtJcXEr4WONRliTnhQBT7fmJWI7Dn8K5H4/RNd/CXxJYHkTaBeoR6g2716NbFyp4T2iMYw5qvKUrP9pb9na7JNr8Z/DJKj5gdZQdvc1Mv7RPwNcZh+L3hxgf7uux/wDxVfGX7CX7LngH4+6V4g1Dxm0+6znskhFsyjgwknOQe9e+xf8ABMz9n4hkuIdVPJ2lLpABn/gNeNh8wxuJ1ijpqUaNPRs9Jb9pb4FpeJZ/8LV8PlnYKirqm8kkgDGCc13ELmVBIpyDg9etfPdl/wAE0P2e9P1WPVYH1nzIJlkiWS8RlBBBAPy8jNfQltaG3t1hBzgAcn2xXq4Z4pu9RHPP2aXulHWvEPh7wjpc+veJNShs7G3G6a9vLrZHGCQASc8ckCuYf9qL9nstsX4w+GicdP7aT/GuW/blijf9m7xDDMMqyWm5SeD/AKVFXif7K/7Fnwj+MnwosviB4pW+N1c3l1E620qquI5doOCM5rz8VmWIeJ9lSNKVGHs+dn0f/wANR/AaZxBbfFjw0Xzgf8TaM/y611/hnxPofijTU1fQNYtLy2lH7ueynWSM/Rl6/SvDrv8A4Jy/AoxSC0i1qFm6Mt0jAZ/4DzXh9zqnj/8A4J8/He2tL3UZ77wdrMu6Ug/LLBuw0gXos8eVzjjBpPG4yhJe12KjCnNWiffMLL5ePypwfjJFU9Dv7XU7KO+glV45EDI6nIZSAVOfcEVbiGYCD1xX0GHqe0ppnPJNOzFMyCozuzuApfLHXHFSKq4Fbt2EY/iTxb4e8D6BceJPFmtQafYWuHuLq7l2JHkgAk+5pngzxp4Z8e6JH4l8IatbajYz5MN5az743wcHB9jXkv8AwUP2y/sp+JrbIO+K1GP+3mOov+Cc7SSfsv6CrkkC91EcnsLtxXhrMWsZ7I1jR/d8x78OnA+lRM7c8VIjZXpzioX49690xWxFNJ5ERLOAAOcniuS+H3xl+GXxNv8AUNM8DeMrHVJtMmEeoRW28PbsTgbt2M5Ktj6V1NwqSxm2l5V/kPOMg8V8o/8ABP7whDoHxL+K+q6bbyCxfxJHZWbscg+VJNkA55ADCvJxFepTqqKNYRTWp9bxKCmcfSiUjyuoqOGVWjGQckU5nQfMSMAZyK7VVtSuzMwfGfjnwz4A0Z9e8U6xaafYxsFe5uZdiKxxgHB5P4dquaD4k07xPo9trOiX8Nxa3kAe1uIH3JIpxhge4NfGX7fHiHxH8ZP2gvDv7Pvg66OLJWe5KMSq3MqlmJ5xhI1HHYsa9B/4JsfFR9a+G1/8K9X3Jf8AhjVHSCBycrazMSoxn+GRHX2wK+ejm854vkex0vD2p3Pp+MZHJrO1fVNO0DT5dU1q5it7aBC8088pVEX1JBrQt+RnPWs/xTo2n+INIu9B1WES211A0M8bDIKMNp/nXuVqrVDmRyQXv2IfCPjTwv4301dX8La5banZliq3VhdiSHcOo3ZzkelaxBbJByO1fI37Hes3PwI+NviL9m7W7phBNdvc6VGxwDKvUAZx88ZRvwavriJwyZz2HQ+1cuX414m6e6Na1LksxFJUYPWuY8U/F34d+DvEFr4Z8UeOdJ0/UtQcJY2d5deXLMzcKEGfmJ7cdq6S9mWC3LswGBjOenf+VfDvwl0q6/ai/b41T4o3O6bQvDl159qWBaPbDmG2UZ6ZffJ7EZpYrGeyqciHTp8y1PuKzdnUNLknvWD4z+IXgn4c6cmp+PvEen6RbSziOO41C7ESM55CBmblsdq6C2TaoUjkCvmP/gqJYLqPwq8P28uCB4piOCBjm3m9ajFYmph8LzoKcVKdj2df2jvgaI1YfFbwyQwH/Mdh6f8AfVM/4aU+BO7yv+FseGRnP3dei/oa8S+Fn/BPf9nvxn8OtD8Q6xpWofbL7RrW4uTHf4BkdAWIGOOa2G/4Jjfs6M7tDDqy5P8Az+A/05rko4nG1Y80djRwpJ2Z7H4P+L/w18f31xpXgvx5o2pzWsYa5gsL5ZpI1PGeDxzXUh+clfrivJ/gR+x98KP2ftd1DxR4BtL03eo2i29w1zLuygbdgdOpNesMMc7ua9bDyq8vv7mElG+hheLfif4H8B3Nna+MvF2n6ZJqU3k2CXN2waVxjIA6Z/HAzit2G6iuIg8UgII9eelfHv8AwVAn36p4PgEmGMd+qnPXiI+tdN+wz+0fdeJmb4LeO52i1LSLfNg8j/vLuMH/AFT55LoACP8AZPOcV5NPN1TxkqUtjf2L9kpI+oVAKjNZHijxV4d8EaQ+ueKNbs9NsYsebeX04SNMnAyzeta8RSRflYHpmvn/AP4KZRmf9lDV1PP/ABMLAgev79RXpY3FKjhlUiYR1nY9u8JeK/Dvi/SV1fwvr9pqNpKCI7ixuo5o2I4IDL3rUbYq4HGK8C/4JxAp+zRpp2Af8TTUSMDH/Lwa97diRuP61WCxTrYbnHUjySsc7rvxJ8CeGdZt/DviDxbpdpf3eDbWl3qQjllycAqmeckcVuqfMTOa+LP25AT+2P4NeJsMdN04ZH/X/LX2jaZaFWJznsa5sHjpVa8qbLnDkhzCP+7Tc54Hqa4ST9pL4HJcyWk3xY8Oq8TFXSTU0Ugjg5DH1ruNULfZHXPUEfpXwD+zd+zX8P8A45fFPXNB8aQTiCztZJI/skoRtwuCvJIPFZ47MK2HqKnAqhRhUTlJn2I37UvwDtj5cnxd8NgjPH9rIf5VveEPif4H8fQNdeD/ABbpupxpzJ/Z18soTp94A5rxiL/gmj+z5AWENpq2WbIb7ZH/APE15D8cP2bfHv7IOuQ/Gr4N+ILg6Za3SfaElcNLaFvuiXHEkTn5fbiuT65jIK89i1CjJ2R91w85JXt0p4CrFkDtXC/s+fGHTPjV8OdN8e2CeW11blZ7cnPk3CtiRD+PP0Nd4g+QDrgda93CV416akjmlFwlYWo5eCakpH5Uiu4RTluEhQu7AKoySfSuDX9pT4GpeNZj4s+HSynDqdZQnPHq2K67xFGzaLPg/eglGf8Atm1fn7+xR+zL8PPj/wCN/F2nePrO4aLTUtHtPsswjwXZ1bPBz9wV8zj8dVo1/ZwZvh6SnBykfb3/AA0f8ElAz8UvDoPvq8X/AMVSJ+0d8EJrgQL8WPDm9zhV/tiPJP8A31Xlb/8ABLj9m2UjbZ6spx2vU/8AiaZb/wDBMP8AZut5xM1rrLiNwdp1FQCQQey+tXCpjp2G1RR9Dx3SSr5iEfN0I78UzUNZs9Ls3v8AUbmOCGFC808hAVFHViSeBRBaGKPySvp1PoAMfkK4X9pxJE+A3jCENkt4ZvwB64hJH8sV2V8RVw+F5+plTSnU5TpPB3xE8HeP7OTVPBHiqz1S1SUxSz2Nwsiq46rnqD7V0MLBod3UAc57fWvy5/Zd/aC8S/s7/EYapLJJL4Yvbr7Pqdqo4AUAM6LnAkH3hjquTX6beEtf0zxHo9trOjajFdWtxAk1vPE4ZZInxtYEdcj8jXBlubrFVOSRrWw8qaujS3BV3MPrXP2PxL8D6p4qn8F6V4z0u41e2ybjTYtTja4jAxnMWcjH04renyFOO3Svin9nYMn/AAUV8a7upu9TBOOozHiunGY50K0YLqRSp+0T8j7VhdyCx64qOS4ULyRgd/SpVJ2Zz1A615L+2H8cLz4A/BDUfGOi2qzapuhtNKSTlftE7kI7eoUAt9QK7KmL9jhvaMhQ5p8p3Hir4k+B/ANuJ/F/i7S9KjIyDf3wjJHqFzk1z3h79p34AeJNQ/srQvi/oF1cO2xYYtRwzdsDcRXy/wDs7/si337SWmN8Yvjl4tvr2PUJnFlAs/z3AVgrSMT/AKtdwYADjivRda/4Ji/ADV7OWLTo9X064bOydbkSY4wGII565ryY43HYhc0b2NuSjF2Z9N2l9bXVsJ4pVYFcjDZ47GpPMJXr+VeIfsm/A/4y/BG51Xwj4y8cprfhuJgdCeWdvNjcnkqvJCYwNpYgHp7e3AY4Fezg3VnTvPcwnZS0MHxj4w8PeBdMk1/xhrljptjFgyXV3MVVQSAMkHuelc7aftPfs+3SDyfjB4YfI/6DUI/9CauO/wCCgdvA/wCzjreVBPmWWc9/9LiHr7145+zL+wT8F/il8JtJ8feK/wC1HvtShleRYbxFjBWUpwNuQcAdfevExWY4iOI9lTOmlSpuHNI+mW/ab+A0Iyfi/wCGlH/Ycg/o1W/CPxw+E/jzVjoXg74i6Hql3yfsthrCyy49doPPevIB/wAE0v2djGYxY6rnHBN+p/8AZa674IfsbfCH4JeKH8ZeDrO/W/aEwiS5uAQFPUDgdcmtsPPHyl72xE1QWzPY9sZUFgCMDrXI/EP4p+BfhbZw6p4/8W2Ol291ceTbzX9wyIzddgxnnHNdSzkrnHNfJf8AwVUs2v8AwD4WhkJ2DxK24g9P3DHI/I1vj8XPC0OcmjBVZ2PqTQNe0zWbaG+067imiuIRJbyQvuSVT0YHPNXmJ4Pqa+Rv+Cc3xsuntLr4C+Mr4i+0lmudIMz8yQHG+Mc5JAKsP9lj6V9dBdyBiOOOe3PSnlePeLhdhWp+ylYTzmjkYqPT9a5Lx18afhr8NNSttN8dePtI0ia9YfZY9UuRA0uSBkHnOTwMkVueIdfsPDumXGrandLBBaQs9zPJwI0RdzsfbHGa/LP48/EXxN8avi/qXxD1BZUtru7MWl2xbKw28bpsjA6cA5PA+Zq5cxzaNCooRZpQw/ttWfrDbymSAEDlh3qSWQBNxHaqeiyNNZRyN1OOP+AipZmbymwcfL1r06OJk8Jzo5pU0qvKcZqnx5+Dfh7V7jQ9e+KXh6yurYkXFtc6uFkj6ZDKWGDUDftMfALys/8AC4fDZXGAf7ajOePrXyBafBXwn8X/ANubxX4C8XJKLW9u72aY27hXLJFCy4Jz3Jr2+H/gmj+z0iBTDqrjAypuYx+P3a8SOPxdZvlex2eypQ0Z674X+OXwo8W3g0/w38QtC1CfOFis9TieQ/QdWP412dvcxTLlTn1wentXxL+0l+wp4a+GPhCX4jfCfU7+CXSis93BPKGdkXnzEYYIZSen4mvcf2LfjHqPxU+FME2vXhuNR0q5Fjfz95vumOUnuzJ19wa0wmY1VW5JsmrRjyc0T24uAu8Hp3PauU8Z/Fb4e/DieC08beO9H0pr0n7Mup6lHbtKQRnG8/NjPY8cV0vmMBkkZGOlfE3/AAVYto5/E/gJ5VDZj1Xhhno1sf616GY4yWGoqUTChD2k7H2rZXIuoFkU5DAEEdxirKKvkFgB0qjoAZtMgH/TJRn/AICKuW7K0ToepzXXgK7rUOZikrOxCLdWHSiRzEnJxt5z6CprdRvO4dqguyxRwHxwec9K6KlTkpOQt2cZrH7QXwa8MaxdaDrvxK0K2vYD/pNrPqADxnA+8Ox9qij/AGmfgayDZ8UfDQU+mpoM/rXxv4o+G2lfEf8Ab/1r4a67vWyv9Tme4Nu2x8CyikXBPfJPNe4r/wAE2/gNLEFNxrYJA4F+vp/u18q8wxdWs1E6FTpwWp6rN+1H8Brc5n+LXhsYP/QUQ/yNdZ4S8W+H/GekReIfC+s217aXQPkXdrJuR+cHB+tfO/8Aw7M+Ac0paS911lyMg36/4c17v8I/hf4Y+Efgiw8BeDrdlsdNt2SATSbmJZgxJPfqa9fCSxMpXkZyVO2h1/3V6dqZ/wDE04+WB1+lMTOf517JkOUYGKROv4UqjAxS0AFFAII4ooAazEHg02nNuP8ADTaACiig5xxSewEEJwZST2p8mO3FR5IMpx16UEgdTR7pEUyOnWJ+XHvUOQehp+n8npQrdCy7RRRTMwooooATIwSDVXIByv61PkeWXqBiCeKDQajE9e1La7cN+NR5I6GpLT+L8aALqjJxmkpyjnOO9NoCA4DIFITk5pKKACiiigCOXvTPObOypTIn51WmObgkUATxEMOahdf4s0tu+QcHp6UEr0NJ7AQzKyv8mAPQ18Gf8FOPht4s0X4s6Z8cbLTnfTzZ21o06qSsE8Dl1346BiRj8c196vvkJy1Zut+G9G8SaPPpXiHS4LuzuVKTwXUAkjkB7Ec8/qK8XMcK61JxgbUKqpvU8e+Bv7dvwY+JWgWsev8Aia10TV3Qfa9N1WQxjzOAWST7rAnNe1aV4h0bX7QXGj6tbXUB6PaXYlQj6g14N46/4Jufs/eLEeXQdPu9BmcfKNMvN0QP/XOTIA6nANeLeNP2J/j7+zxPP45+EfxCl1C3swZZILR2guQgGSSgJVzz93vXmUK2JwdNQktEaSpwm7xPvGAqwLRnPHUGnquF+leE/sVftMX3xr8O3WheLHB1rSljaaZVwLmB+FlIHR8ggjtXvClCMKfxr28Pio18M2jklCUZ2Z8W/wDBTBRH4/8AA90eFQ3RJPoJIq+k9B/aC+Dcmmx+Z8StFDFRuU6goIOB78V85f8ABTWL7V478F2QxudLwenWSCuh0f8A4JsfAi8s47y8j1USSAFiLpTyVGe3rXxsJV1mMnTPSUKfsFzM92f9oH4PgbI/iNpDH/Zvwf5V1OlalZaxYpqdhdho5ow8UiNlXU9CPrXzzYf8E2fgDaymVV1fr8pF9j+Ve7+FdAsvCmg2Xh3S1YW9hZrbQCRsttUEDJ7819XhJ12vfOCcIrY0nmAjx1yK+J/2uLZL39tzwbA6g+bZWysG5yPtDD+tfaTj5MD0r4x/anQj9u7wKo6mztuT0/4+zXl57T50vU6MFKzYWs0/7GH7X0EszNH4T8V/JMCTthR5MByT3imP4JIa+2jLC1uJVIYEDGDwfT8814n+2t8Dv+Fv/B29OkWPm6vpDveaaFGDJjPmRcEZLqeB6gV4j4a/bxn039lSfQbi4k/4TDTm/saHefmaMp8t2Sf4kQHI7MK4MNWng049GaziqzuQ/tKeI7/9q39qTTvg74eumfQPDzul1InKbx/x8y5xyAAIx7lsUnhKwt9H/wCCjUfh+wgWC3tUgiihjGAqiwBA/WvRP2Bfgg3hTwLdfErxHa41XxAhaOSUfOLYElC3/XQkv71xmlwBv+CoN3nqDGSf+4dH/jXNOlOVaNSXU0g0k0j7Nt0C2qhR/COK5n4w2/m/D/WY88NpV0Mn/rg9dRBzCAR0ArnPi8G/4V1rAXljpd3tx/1xevpcSv8AhNOGj/vB8jf8E0viX4U+H+l+KbTxV4js7BZ7qyMP2qcLuxAQceo5HNfVkX7RPwXbAPxI0jJHe9Xmvh/9jL9mjwD+0IviFvG/2zdp1xZpa/ZLkJhXiO4EHPOV/nXv0P8AwS//AGdzCpYa3ux/0Eh/hXhZZPEcr5EdWLUHK9z3rwz8RPBHjKR/+EX8T2V+0a/OttdhtvvWyMSAYryv4I/sofCn4D6hPq3gm01ETTpske7vS4I+leqIcqMnrX2OFlVlT9881pJnjH7dcRP7NPiMAchLXn/t7hrO/wCCdDR/8MzaYhcbl1XUByf+m2a3f200WX9nnxBA67sraZB7/wClxV8tfADXP259N+HNvafAvwbZz+HxdTtBcSmHc0pcCQYdsjkHivksRVdHH853Uo8+HsfoBvjA2lxgdyelfHP/AAU91rTNVu/DXgKxUT3+y7mMCcsomCxovqNx5rlPiR8e/wDgoN8ONMjvfH8cekW88hjS4S2gPzKCSu4Z2nHPPpXpv7Lf7MTeKdWsP2i/i/4xXxLqt0kd1po3+ZFGf4HZjjLLkjYBgYrStiZYtqKFSp+ydz6F+FmhXvhnwNo+i6kxaa00q2t5yxyd6QqD9eR+ldDb/c/Co4BtQAE9Opp8GAWUetfUYNctBI55O8rkinKMp96j60UifdrpWxJ4b/wUHI/4Zm19PX7L/wClCVH/AME5WDfsu6ER/wA/mof+lclSf8FAz/xjJrp/69//AEev+FVP+Cbrlv2X9GB4xqGoj/ybevj9f7XSO2H+7s+gGyVyRTaASRgd6kIB6ivsaexw3RTuIpJHyODnIPvWH4S8EeH/AAbbyad4Y0lLeOed57hYxjdK5Bdyc8knmujK5cknnNIYVYZYfj6VlOlSqy5mO8lsR252Fcn0rB+JXj3Tfhp4I1TxvrRAh021muplB+9tyFUfUlR9a6EoARz+NfJ3/BTv4qf2P4Q0r4PWMmbnWLj7ZqAVslbKBgf/AB+Xbj12kGvJzTE/V8Poa4aHPUsYX7BPg3VPij8SfE37RXi0bp7i4e2sZW6edI2+U47bU2pWfr90P2V/28E1d5fs3h7xiAztkhUWdwGJ90nCn2EhNM+An7cnwx+C3ww0zwCPAerzSWMDfabi3kjCzXDMGZwCcjPvzxXH/tc/tI+Bv2itD0saT4L1OxvtJundby4ZCHhdcTIMH/gQJ6ECvkI1Yp83U9GzlKz2P0OsZle1EhXAxzk9DinzNuU5GT715B+xh8XZPjD8D9K1e+vRJf2Kmx1MjvPFtG8+pdNr/wDAq9g2FoyxHBr7XAVY4rB+h5tSLhVPkT9vTwvqvw98deGv2hPCwaKayu0iu5IwM7kJZCf95SyfQivqLwB4qsPFnhDTvFWnMrW2oWkdxCwOflYKcH6c5rkv2kvhuPib8HNc8JKm+6e3M1lx0ljAZCPc8ivM/wDgnX8TJPEfwqm+HupzN9r8MXzQhHGCLaRiVH4MNvtjFeRTqrA419mazTqUrnZftk/FOf4VfA3V7+znKX99H9g07DfMJZVAJHrtTc1c5/wT0+Fg8DfA6PxFc2uy88QXH2yR2GGMAOyIH6rlvrmvOv2xdUvfjn+0b4c+AGhktDayr9u28hJZfmkY+8cYx/wKvr3w/o1jomlWuk6dEsVvaW6wwxL/AAoFCqP0P5mqoP63i3LoOSdOnYtwjgAda+a/+CmYB+GOgqMZHiWIkn/rhNX0pGevFfMf/BTa7eD4c+HIVPL+JlBP/btN/jXXni5MFZEYRc1Q9D+CXxb+HejfCfw7aav41021lTQ7NXSe6VSMJ0IJ47V1A+PPwdUAN8TdEz3J1FPSvnv4a/8ABP74LfEXwVpXirXrrWFu77SbeeYR6gNu9lGcAjgcDit2H/gl9+ziV82b+2nBOcHUAOPwFeRllTHOK5djStGkmfSOi6rp2t6fFqukX8dxbzx74J4ZNyOp7g96fKRtIzWT8OfA/h74ceCtP8DeGfMSx0y1ENsJpNzBR2J71ruNy7cda+tjzex1OONrnxh/wU/nUa74Khbnc2ojr/sRf41F+1p8FfE/w1urD9pX4WSy201kIX1L7OpzC4QbbjA6qQWRx6e1N/4KmBv+Eu8BWyAgu98B7ktbr/7NX13Folnquh/2RqVpHNbSWghnSUAqylQrKQexXivhJ0JVsbKx6kZKNBHE/spftH+H/wBoPwMurwFLbVNPIg1rTVfm3kJ4ceqPgkehyO1c5/wUZjW6/Zh1WBQcnULAbfT/AEha+fPiV4O8YfsE/Hy1+JXgCOabwrqsh/0c5KiIkmW1cnjcByh9q9l/ax+IPhv4qfshy+NPCt8txZXtzpzodw3Rk3C5R/Rx0Irrq4mp9WdKXQyVGPOpI6P/AIJ4wmH9mzTEx/zEdQOf+27V7exZU+leMfsAKo/Zw03bj/j/AL7p/wBd2r2uUDYeOwr3ct0wHyOav/FPiT9s12k/bL8IbjnFjpvf/p+mr7VsR/o6mviX9s2Qr+2d4QAPJstM/wDS2b/CvtrTc+QOf1rgyqX+3S9TWsv3ImqRn7O4HTbXx/8AsEyovxw8VqT0s5Rz/wBfRr7D1Eots5I7cV+dXwn1/wCP2keP/Et1+z94Utr+9E8q3pYqzRwm4bacOwByQe+RU5rUjTxV2PDxcqTSP0VV0bjcCPUGvIf22fEmj6F+z54nGrMmb/T0s7SNj/rJ3ddgUHqe/wCFfPuvfGP/AIKReH9On1bW/DM1rbQRl5pYtLhYIgHJ4Y9BVP4G/Db4jftx6ovjD4sfGxrnTdFuwraOkX71GI4kVRhEUjID8nqM1zzxvt4KCQqVL2c7s9k/4Jt6BqWhfA5p9VjZEvtbup7QOOqbFBI9AWB/Kvo61JaLJ9KxvCnhfS/CmkWvh/RbFIbWztxFBDGABEnA/Wte3JCBQ31r6PLKbp0FcxrS5qmhLUTMyk896mXqPrSEZ4NesZmN4lY/2Jcup6W0hx/2zNfH/wDwTa1zQPCviXxlc67rFtai4S0Aa4mVM4eX1OO4r7D8UAL4cu8DGbWXn/gDV8G/si/s1/D34/a74ntfHSXkqabPb/Z/st8Yj85k3Z65+59OtfDZtOTxqUVqduGjeg7n3C/xi+FsK5uPiDo64H8WpR/41P4f+IvgnxfePYeGPGOn380Yy8VrdK7KOmflrw5f+CZf7NTRBE0zWFOOMauf8K674LfshfC34BeJ5PE/gW21RLmWAwP9r1LzEKE+mK9XC1MWmk1oc04wPW9hJOTknvXCftHxLJ8GPE8QXJOgXw/8gPXdRsW+UnkVyHxzhWf4UeI4W6Not6Pr+5euvMbywLuTQVq2h8V/svfAzSfjb8HvHvhC62x3a6pa3OlXpHNtciAhT/utjaw7gn0rrf2Fvjzrnwd8dy/sxfFt3tBFdsmiNdvtFtKTl7f/AHX+8nvkd66P/gmNGJdG8YyMBj+07QHI4/1JrV/bp/ZRHxS8Mn4ifDy2aHxToSl08v5WvoE525HWVeqn8K+NwlCrFe1h0PQqVU3yM+nJZVePeDwQP/1V8XfAkiP/AIKN+Mto+/dalgf9+/8ACu7/AGIP2pZ/i54VPgTxteFPE2jQlZRIcNdwKwVZcf8APUHhx6fN0rhfglGYv+CjHiw4/wCXnUv5x121cQ8RWhJmdGHs+Y+00AaMYHYV4P8A8FBfAOu+O/gNPb6FZvczabqFvqDRR5yY4wQxGOpG7OPQV71CMxAe1Q3ttDcQ7JVBXPevpKlF4nBKByKfJVufIX7Hf7YfgHwb8PrX4afELUxpcunyutpeTxM0MsUjl9pxkowYngjgV9N+FPij4C8cWySeF/GenagDyFtL5XP/AHznNcJ8Sf2H/gN8S5Zry+8KJp93KSTe6TdeQ+48ZK/dJ6mvEfGP/BMTxN4ddtY+E3xTLSxfNDb6jGYZOOgE0Zxnk9RXlUnjcCrLVG0lTqan2ZbS7ydjZPOetPAycV8h/sr/ALS3xF8D/EV/gL8c5LlpkvWtbW4vW3TW8wAIjdv4wwOQ3pX13C6yIrAYyBx717OBxscQrbM56lNwPDv+ChJJ/Zp1ko2M3FkMn/r7iP8ASsr9jH4s/D3Qf2e/D2ka7410y3uYo5xJBcX6I6AznGVJ49R9a2f+ChDxp+zVqpYZ/wBLsA30+0qa8g/Z2/YY+D/xP+FGj+PPE8mofbdSikacRXC7QwlKDAIz0UfrXzGO9qsy/d7nZSSdH3j6ef41/CYRkyfEPRgf+wmn+NbfhfxR4d8WWA1Tw5rFveW5O3z7a4DpuHGM9c14TH/wTc/Z9C7ZINTzj/n7FeqfB34O+Dvgr4Yfwv4EtJY7dpzLI08+8s31z068V9DhJ4y/7w5Jqn0OxJ5Kmvl7/gpdEkngHw27KDt8UpkH3gfivp+MFhnHbvXzF/wUzBX4a+Hxjk+Kof8A0TJXLnac8Oka4T4zzL46fDLX/hBpXgb9pz4dO0VzZ2NjFqZQYHmLH+7dj6Om6Jv+A19lfCX4k6F8U/h9pXj7w7OBDqFsJFj3Z8p+A6N6lTnPoM1zGh+BdJ+JP7PVl4M16FWt9R8OQRSMQPkJiG1x/tK2CPpXzl+y/wDFy5/Zj8YeLvgb8V7mSC009bm9gYycpNEhZ1Tnjzo8Ef7RrwcHKphHdbM6J2qaHoH7e3xYNlpMHwc8LuZNR1lFN9ChO6O2yAkRI6GRwMeqbvavA/2lfhDH8IR8PfCBUfaf7AvJtQcDG+4a5jLk49+Pwr0v9kPwfr37QXxs1P49+PrXdBZ3AmiVl+Q3TD93AoPRYIyMj+8VI70//go/YgfEbwXKnP8AxKbxQf8At4i/xrmr05VqjqyNaTVNqKPr7w6GGlQgnkBM/lVmYYgbZjhe9VtAONPUccCP+Qq3PxA4H90819fhf+RacE/94R8VeENZ0Xwx/wAFC9f8Q6zrNtY2kc14ks904VQWt4QASemTX06vxz+Ep2qPihoPQdNVjB/U18n3fwn8N/F/9tfxN4O8UPcpaXF1cu5tbgxyZWGFhg8969Ol/wCCaP7P1whEt94jJIH/ADGP/sa+aoTxMakvZ7HXWhCyuy3+1b+0p4Asfh1qfh3w94hsdW1LVrKS1tLawnE+zzBtklYrngAHAHOcYFa37Afw31TwL8G473XrCW2vda1H7Y0EylXSJUCQ7gTwSBkjqCa878e/8E7fB/hzRH1n4S+J9W0/VLUCS3N3dCaOR1GVU4AIJPANdX+wR+0F4u+JGk6l4A8eM0+qeHmhK3cjDfNbyFkG/HV1ePbn0NaUOdYv39xWXsbI+kH/ANV+FfF3/BVHa3iHwED18rU/1e1FfaLsChxXxZ/wVEIfxh8P4j/zy1An/v8AWlernV/q0UZYNL2h9m6CCmm24Y9Av8hVy2AbcB3Jqpo/OnxEf3Qc/gKsQOFJyRgmvSy1Wwhz1PiY7lGIHHFQXLlYm57HmrWVY5BFVrvaYnAIPynn0rfEyaosUdZ2Pht/Eeh6D/wUx1TWdc1aCytrUs0k11IETJ0+FcFieM5/SvqqP4/fBlI1WT4peHx8oyTqyZ/nXxp4/wDh7oPxf/4KHa78OPEyy/ZL2QpOYJdj5SwgcYP1r3K3/wCCZH7PaxhpodYYlR11Aen0r4rCSxLxEnDa531Y00lc9n0T4xfC7xBerp+j/EPSb13bCW9vfo7MfbAzXZWrQzAMOR1GB0rwjwT+wj8CPAes2+vaNpmpi6tZ1lhkfU2IDr047jmvb7FZUjy47dc19jg51VBcxxTcdkXSSTk06NwYOlRQ9M0+vVIFyfU0gJByKKASDkUAPTp+NLTV+X71DMQ30oAP+WlMQfLS0UAQwZzKamoIB4NFJ6oBrE8jFVGHPT6VPGW7sabLjzX6f5FcMDWBTqzZv0z61Wtxvbb6VMoIbAFdy2Mi9RRRTMwobofpRR9KT2BbmfRUlRL3+tZ0zQWpNP5Mg9xikh/i+lSWGYo8+oq6YFmigHIyKKoAooooAAcHNAzsOfSiigCrP/rzk9qftYdqmMWWwfypcbeMUAUYi0PWnMxYZA5xT2hYnoKY2VGSKT2AbkomW4xXz18Qv2//AAt8Ifjpqfwq8e+Erux0uBo1g1yJWZ2YqGeRk7xg8BgT0r6HCSMMyD6e1cJ8YP2d/ht8aLBbTxt4dt7t1UiK4WXyp4s8fK/Un615GL+sKPuI0p8rfvGh4J+Mvw4+IGkx634R8baXf28qhlaC+QMMjPKkgg/WsT4v/tBfC/4XeF7nUfEfii1LxZZLeO5WWaZ9uFUICT8xOM9BXhmu/wDBLTwibppfB/xC1XTEz/q5YI5wB/vIVJrU8Ef8Ev8AwPpupfbvG/jzUdWBbPkRQCBWHGAxJJI9QDXi1Fjqi5Wjoi6UXcwv+CbWg6rq/jbxF48Fo8NkLH7NjkDzHlL7OuOFP619kxh1rE8DeA/Cfw28NReFPBujQ2VpAuI7eBPlzjqW/iPua2POwAAR25PSvTwOEq0aDi+phVnGc7o+L/8AgpVq0Np8WfA4nkGxI7ljk9czwj+lfV+jeI9IXT03ajbgFR1ukHYf7VeQftW/saaT+094i0nWNR8YajpUmm28sJEdtHNHIGkDH+Ic9MdyK84tv+CSHg+RAJfizfMe+dJH/wAdrw1hsVhsXKSR1KVKdNJs+rpfFfh7y/LbV7QY7m8j/q1XtI1LStVjzY3ltMBwTFKr4+uDXyQ//BJPwYB+7+JtyT/taSP6SV6v+yV+yra/szrrUel+Lv7TTV7i3+WS1aDyjGGz1JyDnt3r2cJWxLlaSOacKVtGe1SxqF+YCvir9r26jsv24fA1zuAC2VoOvrdsa+1FO5Mk54559q8S+Nf7Inh/4w/FzSPijceKtRsbnRRbxrBbwq0U+yTzACW5A68iqx+Fq1UmkOhONNs9ujQSwhD0Pv718p+Jv+CcVprnx3uPFy6xDB4Yu7z7ZNZKuZA5OWjA9Cev1r6stnyoXAHPTNToFPBFOOWxr0030J9o4vQw7Owg0a0j03T4FWGC32JEp4jULgAewHb618jaHcB/+Cpd9Ex48pTz7afEK+yLq0BLBF9eleQWX7Kml2f7UT/tKf8ACRSia7g8pdMWEBVYRLGWZ855AHHtWWJwLjyqPQulUau2e0Qf6kADtXPfFZ0X4f6urH/mF3PHU/6l+1dEi7EChuAPSsjxHYW2vaVPpF4+EubNo5HH3gHVkz168iuyvh5ywTiY05L2tz4+/wCCYus2Wn33i+G+vYog409lEsyoGOJRwCR2xX2IvinQymBrNpz3F0n/AMVXysP+CUXg+UF5fipqAY4yF05RjpxndzVW/wD+CRXgq5iKW/xT1AMSMeZpcbcfi9eFgoYvC3ionXU9lN3bPraPX9IdgkWr2pJ7CeMfyNXoSSoIOfWvjLwz/wAEptI0HWLfWbX4u3Ze2ukdYf7JCcqynDEP069K+yNNia1t1iln8zaPvYwTxX0GGrYqStOJyThBfCeWftlNu/Z914Ln/V25z/29R1S/YMSP/hnywAC5Go32D9JjXc/F/wAB2PxS8A6l4CutQktPtkKK1xABuiKOr5GevIqL4C/DCz+EHw9s/A1rdSXK21xPJNPLgFmkO76dxXmVsvnVxab2NYTUaNiz8WvhtofxR8F6n4K1+1/0S/gIFwo5t5cACRe+QcH3Ga+Yf2RviX4g/Z9+MOp/stfFe7KQyXTPotzI+I1nYsQVJP3ZVGR6MCK+xSzMoLDBwM5rwz9p79jnSf2gNa0jxHpniF9C1LS3QNfrb7t8JO5QuMHercg9s0sTlrw9RTp7F0qqcWme42zq8Q2cDGMA9PapSn7slazPDmlvpGjxabNcPO8VrHH5r9XYDG4+mcCtRQQhBbPFe/hItUk2cz3FgAAOBTv+WdEYwgpXGVIrpewjwf8A4KI5T9lTxHIuMqLbBz6zqKzP+Cc2q2Vt+zJoglnRP+JjqO7cwGP9LbHevUvjn8JLD43fDTU/hvqeoy2kGpxRxi4hGWiKyK2QM8nIr5ti/wCCTHg9dyD4x6mmD8wGmcA8f9NMV8di8PiIY51aauddGpTdLlkfXS+JNE6HVLcHHQzL/jUtpq2n3bGO2vonOTwkqk4/OvkG5/4JD+DpkKf8LqvwSOraUp/9nrof2d/+CbmkfAf4s6f8UrP4qXeoy6dHMq2jaSI1YyIFGW3nsT0Fd1DFZjzpSjoQ6dBbM+p0bIyOaceRjH4Uln/qgZOuO9Ocr2P1r34L3TnKct3HDC000gRVUlmJA2gAkk/gM18O/DiWD9r/APbh1XxpqCGfQdDBNqDlkNvCxjhXB4w8hZyO+K+yfHvhSXxr4K1fwlBq81nLqVjLbG8tz80G8Bd688nFedfspfspaB+zLoF9puneIG1G71G8SW8vJYhGdiIFjjwpPALMc+pr5/M8NVxWJjDodOGqKnFs9Gs/AHhK3txBb+G7NV9E0+Af+y1T8U/DLwVr+mS6Xqfh+1KyoyOrWUYJVhg9F9Dn611ccPygsDzTpLTcMjBz6iuyeS4ZUuVLUxjianPc+J/2KdZvPgR+054w/Zx1ySQQ3LPPpomJGZYScEZPLPAV6f3D6V9qW8hltuWz/wDqrxb4ifsp2HjL9oHQ/j7pHiQaZf6ZPCt1AltvN0EDISWHQsjlfwr2iyRIoVj9B/SufLMLVoVWraGlaSlqR3CeZHhRk9q+JPEXig/sgftea/cPbFdF16xkvIo1UhTuUyKo7ZEikf8AAvevt9lByPevGf2rf2StM/aQ0+xkt9Vj0zU7AssF/JFvVo2xuQgdTnkVOZYGVZc0FqVRqqOjPLf+CfvhTUfiJ4/8RftDeKkLTzztb2cp/inf553HuoKp+BFfXkCgAdiPT0rjfgj8KtF+DngDTPh/oMhmisLZhNLtAaeRiGeQ+pJPHfiuyjXOAe9b5RgnQpXnuRXnzT0G52g49a+VP+Cn1yP+EL8KxAnafErk+4FrIf619Ukk9TXkX7UP7MWnftK6XpWj6h4mu9MTTL9roSwQpMXLxbNpHGMfpTzShUr4Z2Fh5KMzd+A3iLQ4PhB4adtTtAx0K0+/cID/AKsH+9xXWyeK9A2867Yjjk/bI/6tXy2P+CUXhCaJI3+LGpEKoAB0wYH4eZUcv/BJnwcgLp8Urvr/AB6Un/xVePhI47Dxso6G0/Zyep9X6ZrWm6i/lWOr2k+OCsU0bn/x01dKE9Dn0rw39mX9jTTP2bfEV/4isPHD6l9ttUh+zvZCMod2d3BI717mU2D5pfx9a9+g8RVpe8rHNaMXofG//BTWy+0ePfhqrLndfXQ5HXM9oK+vdMTEHysMZ+8T0968u/aH/Zq0745+IvDOv3/iOWzk8OXbTiGG2DrOHljfBYn5eYx0r1W3Rkg2tjJHODXnYTByjjJOSN5VE6XKcr8YvhV4X+Lngq+8F+JbEPbXsW6OQKCYZsYEqf7QPP0r86vE2t/Ef4CXHiv9mXxaHNre39vcxjJEbvHMrxzxkn/lquAfdcdq/UADIxn868V/as/Y38G/tMWFm8+pNpWsadKPsGqpGCQuQSh/vKTyD9axzPK6lR80EXhq6hpIk/YCkjl/Zt0ueI4V7++KkdP9ea9ukGV6dRXC/s6/COH4JfC2w+HX9r/bZLRppJ5wm1S0j7yAPTnFdzJzkbjjPpXp4HC1IYTlehz1ZJ1bo+GP21JGH7bng2PHBtNIGfre3H+FfcemqPKGB2rwr45fsmWfxW+N/hr4ujxVNaPo7W0c2n/YAwmEEryD58/KSZD+Ar3q2jCxBRx+NcWX4GcMVKXmaVKidOxHqjBbdwPQ8ivjb/gm3Mt98VvHwlUORGvJ563MtfZVxbieJlduCOc/lXjv7OH7Kem/ALxl4j8T2Piea+/trYptpoVQwgSM/wB4HnJf9OajMMDOrikPD1YxpyR6ve6ZZXUMlrcW0bpIpV0ZcqwPBB9q+Gvibb+KP2Dv2hYvGHg+CaTwtrMhf7MMlWhJYywN2DpncntX3mQxGOnvivO/2i/gL4d+PXw9v/BGqEQyuVks7wR7vs1wAAr8DJBBKkelPEZW6cVKmiKdfmdmdL8PvFmieO/DFl4v8PXyz2l/bJNbShsnaTyPcjkH0rehGQDj615p+zF8E9X+Bfw8XwNqnidNVMNy88UixNEkAcDMUYJ+7nJzxXqMSKUGOwr1sAp+ySktiJ/EJQAScCnbfn6cUgHQ+9eiQZfipCfDt4MZxbS4H/bNq+O/+CaWtWcHjPx1ayzqCxsiAzAA/POO59MV9l6hAt9p81lLIQsiOpx2yCP618kT/wDBKbwnc6rPqK/FS/i86UuVj0wEjPIGfMGepr5TM8PWniVUpxOzD1YeycGfV39qWG0M11GAe5mUf1qNtc0SMgNq9qPTN0n+NfLf/DqTwnNHj/hcmsYzznTV/wDjlNH/AASX8Byvif4x62QTz5dlGp/9CNaUp4+y0M3CifWsLpIA8bBgRkEHg1y/xlVW+GeuxLyx0e8wB/1wet7RdMg0mzg02CVmjtraKFd3XCKFycfSqfi7RE8R6JeaFHOY3vbSaEOF3YDx7N2O+N3SvQr0atbDNMypOMKtz5p/4Jcwu/hHxhcFfva3bAH6W9fU01ms67Nuccj29/0rzf8AZY/Z3b9nzwxqmgf25HftqGpJcvMlsYgmI1QLgnk8ZyOOa9SVVwDnj3rny3A8lFxktyqs+ad0fE/7ZPwJ8SfA7xvbftQfB+NoIkv0n1W2hX5YJsnc5HdZAcMOlc9+x340b4g/tnX/AI0liEZ1e2vrkR5+7vMZxX3L4i8OaT4p0a78Pa3YrcWt5bmO7gdQRtYAEdOvORXhvwD/AGGdK+CXxfufiJpnjF7i02SRafp/k7XWOTaWErnrjjGPxryq+VVqeOTj8J1060PYu+59CRnfGAMHivJ/2lf2krv9niPQ9SuPDE2oWV5fSQahcYGYUVcooPTex5AOK9bgVcYOOBWZ4n8M6D4x0iXR/EOkQX1pOCJLa6hEiN2+6e9e/KnXp0LQOFODndnIfDj9o/4XfFPTorvw140slmdVMlrLdLHPGe4Kv1x6iuo1bxd4a0ixe81bX7KCJUJaWe8RVA9Tlq8B+JH/AATi+EXiuRr7wjPqWgSnny4Cs0I7nCscr9Aa4yL/AIJaWtxNv1T4s3kkQcHZ/ZhY7c9MNIRXiVKuOfutXOqMKK1RzfibVdN/aN/bcs7j4Zo1xYpqNq0uoIh2Mlsm2Sbd6H7oPfHFfdVtCUQLx6jFec/Av9m34f8A7Pumta+DdMlN3OiJdahcgPNP0+UlcBUHUAdO9emFdiYDZPeuzKsHWhJzmZV5xkrI8J/4KIqz/sxazs6rdWJ6j/n5Wl/Yr8TaOn7Onh5LjU7dGjW4UrLcopGLhj03ZFd18evhJZfG74Zaj8O7/WZbRb5Iv9JjjDmFkkVxwetfPcP/AASh8FOR9p+Kd6zH+7pUY/8AZq4cXhcVDGc8I3Nac6fsuWR9RN4o8Osu467Z5I7Xsf8AjU9hqem6hIY7PULaQjr5U6Mf/QjXyvL/AMEnfAzLtj+Kd/8AQ6ZF/jW38DP+Ce+j/Bf4rab8SdJ+JM12+m3EgezbTFQSBoiOWVsDlhg13Ua+Yc1nExlToW0Z9OhO4bP9a+Wv+CnsqjwP4UtVGd/ilTj6W7n+tfUluryINz9Byc5ryr9qb9maD9oux0fTf+Euk0r+ydTe6Mv2TzRKWQJtHPGM9a6MXh6tairoilNQlodV8GXST4V+HwJAQdEtSSPTyhXj/wC1p+xhd/HTxnZ+MvB2o2tnemBLbU2uB8rhGykn+0RxkdxxXvPgjw3F4R8J2Hhdbjzhp1rFbNO4wX2rjpWrEibCSuMdMiopZZ7TDpMpVnGocl8JvhfoPwh8D6b4F8LqWtrGIrNM2N0zv80kzepLke4HHavm3/go8uPHPgqYrgfYL0YJ64nh7/jX14Auck45yeK8o/aG/Zd0r9oHX9C1HUvFFzpsWkLKJI4IFYzJI8bHn+HlMetY4nLZKlaKLp1P3nMz1DQATpy47pGcfRQanvJWWFztxweaksbZIYRCv8KgA59sU2/ty0RGeCuM130cNUp4LkMpSvVufGvgLUrOx/4KCa619eRQp9ovAZJ51Qf8e0PGSa+rV8ReHkTzZNesSBzn7dH/APFV87/HP/gnPonxl+JeoePLj4l6rp5vrpZntktI3jRiirhec9FHWsi2/wCCU3h+3iESfGXV8gc50+M/1r52NHGUW1CJ1SVOpa7PYfjn+0F8Ovhd4Du9a17xhYPcxRM1pZw3Uck1xNnMaKqk5HOCe1eEf8EzNI17xH4l8W/Ee7ga3guYoLQELtDzGZ5mGOOgOD15rd0r/glb8PDqX2jxF8RtYvQkikxrYRRZX03ZPH0r6U+HPwu8IfDDwnaeDvBelxWlhaD93bxsM5I+ZmP8RPrV4XB4yriOepEcpU6dLlibyALDtZu3HNfFP/BUhxF4y8DycAJa35/8j2tfbbiNo2OASOteI/tSfse+Gv2mLrTrzVvF+oae+nLPDEltCsiOsjxsSQTn+EY+lermuFrVcOuVao58PNU53Z6j4f8AFegLpUTTa1aZ8scfak9B71ZPjLw+cqmu2owe13H/APFV8qH/AIJC+ApY9r/F7VR9NPT0/wB+oG/4I++AEkLL8XtSbJ6NpqdP++q4KVXMKUFGMS3GjJ6s+vdN1nStRQi11S3mYdRHcI5H4A1NIv7hgR1U4NeIfsyfsY6D+zJrmo6poni+51STU7WO3dZrVY1hCtuzkE9c17fLnyiPNHK969Km8VXoNTWpjaMZ6HwvpFza6b/wVM1S71G7jijFzOA8sqoP+QbbAckivteLxb4deEY8Q2OCB/y/Rf8AxVeA/GX/AIJ4fD34wfEjU/iLe+MtYsrnUJUlnigt45I1by1T5ckfwoM1zP8Aw6b+GoUbPidqmcc79OiP/s1ePQo4vDzlyxOqbhUSufUcvivw4gDf23ZHkZ/0yHP55rR028tNQhWe0uY5Y2XIaKQMD9CDXySf+CVnguH/AI9/ifd8NwH0pD/Jq9+/Z7+EVr8Efh1a/D6z1d76KC4nle4kiEYG6VSBjPTOf1r2MHWxcp8tSOhzyhTS0O/AxwKKkoAJ6V7pkOjxk59OKaMZ5FFAGeBQAUUA4OaKACiiigApCcEClopPYBpPHfpVcyN3qcAsarYJGcVlCnYBY/8AVS56Yp62/oKKVeo+tbAT0UUUupmFFEf+p5opjW5SMmc8GhOn40rRY347dKKCxsfepYSM1DbJk8mnRAnOKmmtGBdopNPiJhf2FLVAFFFFABQDjkUUUAOX5vvUSdqRWxwaXdu+XFADSPUVDj/WCpiCOtHQY9etAFTaxPNKAx+Wp8Rf3KW3wpOaAKyxbudv6U9UbbjFTlQaZUqnHoAijAxUbDI6VLTWG4cj9KdkAyO0jERJA6cUixYHGak2jyt3vTg4zgNUOlFsCPYW6Z/OmMhJxk9al+z98U5IQBhhWcY+QCeV5fPpUUUCsxyDjtVhgS3SgpgcVt01ArIojfC1MMdfWjAyTjmlqKegChSRkVD5ee/U0tOUJjk1fJEd2RshHAqOO3XcZOPlP5VaJJGf3eaZbr98+9UIWBRtYeop/lZABpOg4FNxzwf/AB2p5YdgBoYskE80xISnzZH51LQRkYp2QFR5AVf5B8wOTipYWLAH/ZGKa0eeCn6U+BQCODRypgPKsTnio3hwcgVaWNWoMK9cgGkoICpH+5TIyMntVm3Jx+NIVIog4XPvTSsBLuT+7+lNpcn1NJ1pgRC2C84waYYVCurfxGrBJPWislTYEHln1/Wo4kYHJBq2QDwajK/usD1rTkgKyHpgfKD9KGUFSPaoVk2E4IqZTkD6UxkUdrnOR2xzSQQ7ZOBgDpxU9FKyAXkcUFieCaGznmkpgMaBCOKIYex9KfRQA0xg9T+lIYwB0p9IxwKAGBFAGPrijOOc0Rlh+7PT1NJ5WQcGgBhxnimRRHkgVJ5B/u1LHDiKgBnklW+UcfWmMpIGelT42qRTQD5Z+lLlQEaLliQfypDA3901NBGRx0p3SmBnmPDZI71Ii9FJp5hJJJAp8KADmlyoBI4xtHPFNFspxjHHvUxUjrTIoD1NFkA2EbUkIpxldutSCBW6n9aXyAf4hTAhVM/eJqWNdoxtxUmwD7xptADSp3ZGajjwrMSetTscnNVvrQBOAMZIFNaNGOQxyO4Jp8X+oOfSlg6H60AReXjpuqWH7n407Z82c0KMCgSdxaY/3jT6Y/3jQMrNGSCOaeloi4OeQOtS0UcqYEEQC8Y7U7bxknJ9c08xqTnH6VFt/wBoVl7JJiWwvlADco9/rSQpn/8AXUqqSoB/Gm20O5uc1qMkji2jaBjFM2N6U8EjpRQBCYz2NLHbjpj6Yp0UWeT6U5RgYpWTAZDEscnJwMGoooyxwfTvU245zTZFyRxTFZCiGMKcY46imxxxLgkjjpT4PvPx2GKXzPal7GD1EpNDI/uD6UtJu/2T+VAcdc0WRRDJCHbJNOFvjGD+tSeV7Gjb/tH86pwvuYuqMZCpPHTvTY0yDtXr6CpxE/znd1HrTYQQMbayVNI2CCNkUg8HHFP8sEgselOorQzA88HtSFQRiloycYoKSZGLbahbPNMSPqOanooKEhQRjb2pXGT+NFR0AMaPc+SpxQYx0yPzqTA7mjYDxkc1n7OIFc2yEFd4z61JDa+VggjpT0iIL8fTiniIADJqqSSQEcaffyO+eaZ0qxjPFJ5SHsKp6gRxDdke1I0RAz2HTmptoHAGKjKYzwawsuwECNsz71Gwd2JGTjvUjLt70Qwly4zTh8QEKwDJ5p6oQM8YHSpooNqnI796ljgBPSnyoCps559aWKLPCjIzU5jy33D+VFsMcYrSMbagTL0H0oBwc0UUwHqABTSMHApd235cUf8ALOgBoJHSig570UAFFFFACeWvrS0uD6GgKT0FACz5VnxcduBj2qpAf3RJ/WrTdT9aYg5zigzIsH0NJ9KXIxIfpikoNCdeBj0paba96Ve/1oMxaKKKACqjdT9atMeDUFBoMj4ioRvm4NNb7r46g9qSEnp3oAntiwBx61atf4vrVW0759ascYApLYzEooopmgUUUUAFAJByKKKAAkk5NFFFABRRRQAVCP8AV81NRQBXpydfwqXyh3z+VMMPPT9aAGkEnIHekCk9BT8Y4xUlABRQRkYNID5Yzz+FAC0Unmn+6/5Ukcon4MZHvmgBTg9BmmUu8R5ixQA3UCsx9CLpSqMnFSiKJumPzo8oRAgjrWgiGnW3Hm5pIgpaTn1oicAOQRzigCejAHQUUxRk4oASipPJHfNBhx2NArobGOOlO2f7P6UucHgYpv773oGLRR9aKACm7U/vfrTqi80HpEfzoAlpQxHSm7x6GmUASUUkX9aWgAoIyMGo6PP9qAG+SPalt/6UtFuVHm4FAElKvUfWkoBwc0AKSc9TQCxOM0EfNgCkBwc0GYUU3zPaiPOOaDQdUUcvXdUtR0AMYRE53frT4ZTkU2JemRT4YMUAPooooAKKKRPu9aAFooooATywR3qPGB8oqWo6AHQnLOadgDoKROn40tAC849qUNz8q02gAnpQAr/eNJS8saSgAooooAKVTg5xSUUAO3bvlxSg57YpoYjpSUASAg9DTGxnikBIORS5PqaAEAJ6Cgg9SKKKAImBI4pIs4HHelafJ2g/pTosEZxQAeZk8L+NJFLtbkUsYVucVX/j49aALdFFFABT2lz2plFACbB6mloooAKjO4HGKkooAi+Rv+WxqQRgnAqPAA4FLbSYxuI696AJcjuKN3sPyqTcRzmOlD8ciOgysiGiiigYUm9c43UiSAjp9KRoge5+lA4D6Kr1N5oPQZoLHUAE9BTjKTFj2psU5j6jNAC4yfSm7AOhNOJJ60lAEGxvSpwQeRUdPTp+NADgSOlJRRQAUUUUAFFFFAEdORcfN60uxfSloAKKKKACiikLgdQfyoAWgAngVH5x65otpoRzmgCTyT70Z4xTg3YH86bQAUUUUAFFFFADt4z0ppx2oooMwooiP7oH3pIh870ARPjccfhTP4PwqXAzmkCgdKDQdEMZp0JCw7O+TRHGCzn2zQAB0oMxaKKKT2Aa3U/SoanIxk+1Vv8AlrgfhQtjQfaKTG596aoAuvSkAHQnvRtJ5B+lKnqAAgZJ9amg6GqeR2NWYjnn2qgJ6KIDnIFFABRRRQAUUUUAFFFFABRRSbB6mgBaKKKACiiigAooooAasBjGN3607ayjnJoooM+QKSJPLyAeMUtFA+QCcnNQqPL8xjU1FBZFB0H+FS0UUAREA9ai74A71KB5Q5qWgCJPuiltzkrTYmY4+WpYz0+tTTAlpCcr+FJv9+9BZh1FUZiN1P1pKUhupFJQaBRQQR1FFABUcERJ+Y/rUlFAD/smT90/nR9l/wBg03J9TSUAFFFGc80ANMY7GljjxyVoT7opaAETp+NLRRQAUUUUAGSORUMUxzhvWpqTap7UAKDkZptuDiQ+1NEPt+tTWsfbFADfJA9fypE6fjT3JBptABSRqsfI9KdgYznmkoAKQOCcUzyv+mtFAEvl5QNn0qEriYAetTQn5cUo4HA78cUBAbRSjG7j1pKAE2+5pXXCZoooAROn40bx6GjYPU0ygB+8ehpYf+WlR1JQAUUUUAFFHXqaKACiiigAooooAKctnjsabRQAUUUUroApxjwM7xRH3pvSmZkFpETE5PpTooxnJ7U62XmQGn0DhsFABPQUUqttNBYbWHakp0nam0AJvHoaWm+WOxpYYsc+lAC0mweppaASOlACbB6mnCyYdMfhSUoHIoAeYcjHFR07H/TSm4J6CgzCkLAHFOUZOKY4Oc4oKiMCdhcGpFbd2pkaAHmn5X1FBRH5LU+G3HcGnAg9DRQA7y+2f0o+ze1NooAKKKKACkTp+NLRQAUUU3/loCKAHUUm8ehpYpiP8DQAUUUUAI/T8aWiigBE+6KWinxEc5FADASDkUUVEZ8cZoAWKLqxFAh2nhcU+I/ISDTfIP8AdoAkJ54Y0lIn3RS0AFFFFABSr1H1pKKACjOOc0UUGZBdsd02DximWZIBOe1Ev3s0WY/dc9aDQmooooAkooooMwoqSo6AG5+Z8dMcVSQ+UeTjmrnOTxmqzRMTnYfwFZmhLECOvpTI2PlHnuanwxOfIqGbO7mqgzOFyqOoqxZuTOQfSmsCRxUFLmZoaBfZ0/CpIps89aqwiBQ+JuvrU0MePmJ/KrMySiiig0CiiigAooooAKKKKAETp+NLSJ0/Gjy19aAFooAJOBRQAUUUUAFFFFABRRRQAUUUUAFFFFABRRRQAAZP/wBam2wJLcUQgxkeVkfWnrASMmQZPU1EEAA4OTS/7f6UmCG9aCCOoqzMMr/d/WkooAzwKAFf7xpKVjk5FJQaBRUdPilGc0AG8ehpSQOpqOigCQ5xxUe7yuKbE82cH9RSYMXzAfXFAEiyr6fkKdFNnHeorVzgZFPhHy0APooooAKKKKACiiigBP3HvS0UUAKCR0pKKKAAkk5NFFFABTfLGetOpokGOhoAdk4xmiiigApE6fjTKKAJKcp/hNMjOBn3p6DvQA2o6ki/11R0APTp+NLSJ0/GloAASOhoooBIORQAeWP7ppeh5FKr9iabQAm8ehoEinvTHUeUT7UW0sQ7fpQBJRRRQAUUu04zigAHqcUAJ17/AJUU1BxnFOwD1FZcgAOenagnJyaWzXksetD/AHjWpnASiilAycUGggBJwKKKKACiiigAooorMAooorQABIORRRRQAu9vWjcw70lAOORQA5Tk7j2pCfmyKQEg5FFAkrDTEpz1/OomjU87hU9IVz6flQMgjxxToM7uaaR2NSQd6AJKb5ntTqj8r/prQBCzc5U1LBKPukfWgwZ6g/nQIAOg/WgCYMR0pKKKACovOzHyvNS0UAQBiOhpUIA60Mnp6VHh85zQBaoqO3+6PpUlABRRRQAU0yLg8GnVC+c0ABIjhwMniltCCpz+FMhBOAKmgyIce9J7AJb5IlI9sVKzdhTaKYDP9X3o3HO6pMH0NHz+9ADd6+tKnEWPej98n0o8ol/3g69qAClX73SkbEY+X+dCnoaACo6KKDNbkMJH2a44+n50gyCMH9aQkEmo6DQtecAcHH5U2OUMMnPWq9T2uN5+tAFmiiigzCimx7tvNOoAlBI6VWqSo6AE2/7R/OjC9cUtRMCRwaDQhaHJ600Lg5zU9pkS5lNM8rHY0AMqS1PY9qjoBxyKANG3OAaH+8aiycYzT45hEOaDMWktz+8kx2FQ7k9D+VSW6GMZH40Gg+iiigAoHPSgkDqahtT5SgE9+aAJqB164pP4PwpwAxyaAEBI6UUHPeigAooycYooAKKKKACiiigAooooAKKKKACiiigApE6fjS0idPxoAWiiigCKLt9alJwM1GTgZpof+8KAJov9SKKig5AqWgCOin7B6mmUAFPTp+NCfdFLQAEZGKi833NS0UAR06MADj1ptPTp+NAC0UUUAFFR+eT0T9adayk9qAHUUUUAFFA69cUu1j2oASiiigAooooAb5S+p/OlibfgDOaWigApE6fjS0idPxoANi+lLg/88RRS5PqaAEpIz3PrSg4NRmXnO6gAopQCegp8anoaACKLv/OilPB4NJQAUUU3zPagB2//AGv1pE6fjTKkoAVRk4pKcr9iabQAm8ehoDjI4o2L6UtABVaOIDoas1HCMg5oFDcdbrj/AJadDTqKKBkcPapKZEfM4xjinJ0/GgBacNq/xU0Eg5FFACscmko60UAFFInT8aN49DQAtFFFAAkRHOaROn40tKBk4zQAlFFFABRTgAI6bQAA4OaPPyOlFBAPUUAN3jpim0VGjAtwaAHRjvTrUYLg1JRQAVHUlFADfLHqadRUM5wOD3oAmooByMimwNlnoAdRSg4OaSgAoqOigBIDzTxID2P5URjC06gAooooAKKKKAGwp5fOKXywDkB+KWigAoop0ZBySaAD/wCKpGJJyaCcN+NRkknOaDMeh/dt+lAu23cpRUdABRRgZzRkeooLWwUUzzfcUGQjtQMioqYtkcD9KhAJOBQAwKT0FPgxz60+KE4zyTVmgAooooMwooooAKkBxyKjooAjop+wepplAB5X+z+tFR/Sk23P94fnQaClB2xVepd7etONvDkDzetAEFPtDx3p/wBkGfvHFOUcgUASEA9adHnHNNp+8ehoAWigEHoaTcM4oAhNtnJBP50xIm3ctmp/O/2DTYFIwD+tY+8Ao54qYcndtqED0FS2n+pOfWtgEooooAKKKTevrQAtNLEn5aUuvamWs0JLknBHrQBIM45pAV7EU0MwGfOH5VHDdRKZBSsgJfNX0P5UoYN0pvnLTPOP/PIfnTAcYrjGRN+YqSoWvSTwMfjSJddmvO3Q0DgT1FEhJJJP402K7OPmNLDf4MgFK6EPMYHzZpoYE4FP/tBiMFR+NVxIRzkUwLKdPxpaZFNC4+YCmWzAk0AKRk8ilHTpipMjGc1D5nPSgBwAHQU6I5WnVDAcECgCajbD/e/WimW+D5mewoAfRRRQAVHUlJFGc5YfpQARnAz70tGTjGaKACiiigCMeQnINSQRYNInT8aWgApE6fjS0UAKpwc4p9QAHPQ1Kh7YoE9gO1Wzim07tjDUnz+9ALYSilwfQ0bG9KBiUUUUAFFFRQnPIj/OgCWiiigAoBxyKKKAAEg5FAJByKKKAAknk0mf3ec80faRGMoRTIpmbkr3oAKKlyx4zUbJs4oASinR96dQAkZwM+9KOvXFFFABRULTnOMiktpskEn86AJ/pSQ8O5pxlHdDSUBAAcjNFNiOVp1AACExgUUVF5xA6/pQBLRQASOlKFJ6CgBAMnFSVHUUQxyZjxQAtAJByKf5YPTNNMHfn8aAEoojgOOf5U4oMZBoAWMZGPenL1H1oWPAGGp9ADV/3KbSgE84pSGbnbQAnbr+FJSnPY/rSUAFKBnvQCR0pPM5+9QAmweppq2O054x9akyfU0gOORQAUUuxvSkoAKKKKAIZ+/40z+D8KskA9RVe1Hycj1oArkjuafp0xzjdS/Yh/EKlWyKnISgCeikHnkZwaWgCOipQGz0o6//AFzQAlFFFABUJl3nI7VKWAqHcc7qAF/0gdBTbWeE+YpOM980G6I+XzKqRueg9aALOSTxMaPNkHG6jziT1FN+tACm87GQUqT7P4qrmHPWL9aOS/JoAn3t61FUlJ5R9/yoAXOOc08XgPY1DmX1/Skhxg5FK6Atbv4se1Q03zP+mtOpgICU4yTQ0ue1LTBakgY5oAX/AL5pIf4vrS/ZDjlamhgxgH0oAsUUgI6A0tBmFNtcB5Nx6U6mQghpcDrQA+iiigAooooAKKKKAI6CcVJTTEp65oBblAH5iKkhPzYzTDCSc5qzaWxTk96DQkjbgDFL5Q9vypQMdfWloAjpGOBnFLULbs8ZoAUzPnH9KjjlI68UKOpx3pmDjNAFmJ8jk0vmNnNIATyKkNtgZyaVkBGZCBnFP+0YI+Wk8j5uopaYD/N9zR5o4zn8aZRQZjWuByAKiMpJySKUjPmCmeQ27GDSexoLTd59BT8H0NR4PoaFfqAGUj+Gmj6d6fGpJPHarBh/d8ntTArqoK/WkJJ61IqDPK04hccigCCj6VJTI4s8EUAOXO0ZoZiO1OMUfr+tIbT5eCalKzAZEckikljAGQKl8lh0WnGE9hVAU7Y46VcgmAOWX8c1HHHz6UsFuMk5oAUXrZ74pTNEedv6UfYv84qQ24zyv/jtAEf2sjgZpPtfoak+yt2ipkNgfKIJ7nrQBItwCPvU0Tt1AH50i2GeABSjTxGwIFAFk3jCLHtTY7xuiDPHPFN8gf3jR9nOMcfnSsjMfnjNPhuAMqP1qpsg6ZqQA8AUaJAtwM55JpryL5X7oHjrSGMHq4+lTWQRYzgfpTNBq36+WARg460GU/d+0pUu393tz2ptADOQeD0pokEhyKcn3n+lOgQLEB6mgBSSeppN49DSmML/ABGk2D1NBmJ5ntS7x6GjYPU0tABk4xRRRQAAkHNOD+optFADzLkYxUXmDsKcTk5NQ7fm9qDQmqKL7q1JbjDMPeloAKCccmikiw0AoAiW4GcBh+dS71xUMVsehFTfuAcHNBlAWkY4GaUEAjNOK56fyoNSkSc5qW2ICyfWl8g/3fpUgOBj+lAC0hYS8Z6UtBJAyKV0AxcYPNMh6j6VJ5sw/gpVbd2pcwC0Uw9H+tPjx5HPpVAQEFTSGbBxipvKB4z+dIbW4xu8tMfWgBwIPSg88ZoGccjFRNB3x9a5NbgIzNDkZzRFcFuSc/SkkXEJ4PHWltYh5fPXtXUtgJTIBwQfyo3qOgp1FMAM/k8kU8Xq4yIqZQDnkUGYZOelFFFBoO8z2o8z2ptISuOtADvOz0U1F5wPAYU0wgnkGnRReXjIoAT7S3979aFlzzu/WkWI5+7UoQAYoATzT/k0/e3rTGVCOD+tNoMx28+gppf0xSlTjJFNjRQQcUGg9Zs9D+tNJ7k0kanHAp6Q99v60ARicjALCnCfkcd6T7Ec5wKPIx0oAmLE96bvHoaZUlBmFI4JHFMBzyKkAJ6CgBi5APFJkjoaep272z+ZphZCfSgAo83/AGv0pFfJ6UirnkigCTzZcY4/OnVC2R3/AFp8BJByaAH1GJ2X/llmpKKV0BX87PSXHtipYrs5H0qBl7gfpSbWHamaAZHzgE01t38Jpalb91nIHSufnAqlD/e+lIE9D+lWjAM5puwdjRzgV8kcD+VKpyOatRoMc0LbqTyBXQAwWuejUn2bZ90Zqa3AAkwalwPQUAUvKOP/AK1TFSBk1MFC0tZwApEAnNLSle46Ulc+oCrH8vWkqQRdsUluP3JBHc10U9gK7RYP3qsQdBTCOxFTwrwMitAFoAJOBS245fmnbf8AaP50GYzywc8miP8Ad8UrgA4FJQAoYjvSxOPMdabSgE9BUxASJxjaTyO1PDKeM1BZNuZz70kB/fyf9daoCzRRSZUHFAC0UgK9AaSPvQA6iiigAIzwahg6jntU1FADBCB/EacE9CaZThMehiFAC7B6mj7P7j8qWo6AHeUPb8qhFn61JRQAU8ygnvRsHqaaJVztxQAgPcGil81emPypiv8A3jSsgHUm0Y20vGaKYAIRjBUUVJSr1H1oAijjwOtFWJ+1R0AJx0/SoSWHS7H0xUmT6mmtuA4oAZZscSc+nNSQ9X4qGx3YkxS4+bPtSbsVEXyPQ1JFa8ZJoill2kentTwM8kc0yhYYwIwPkpAFYA0tLHKoLqpoMxuxfSmhSRwKfTSZl4z+lBcBojHULRAPT8KlUA8M1Kq/xFqBibDTtpP3mo3DGaYST1NBHLqISQOBQg7e9GPn+tKMRnGM0FgYQO5pPK9jT35OM00gjrQZgEXPNPBAGMimUj52jHrQA4ptHFNQ5UGmU+PGOfWgBEl5xmgOVOFPU0r528UyktjQnXmPOO1MpAp8r6UeYOlMBaVTg5pnme1HmDOCKAJI+9Hl+9M3rT1fsTQZgy+i02lyVOAacowMUARGHnAJ/Ol8qdeR09jTmfBxjpULG73cynHsKAUCQSk9/wBaBKT0P61H5XsaEiIyW9KDQlqLAzupaKAHR4K596dUXkADv+dM6fL6UAWKarAF1zTfJJ6SmlRSAeeaAH0UU0SqTigzHUoJHSkooAKaY1PGTSCRQxBpfMHYUDhYdRSRQ4XPNKQQfpQWFNjGBUhICVGsxX0xQQ9xSwBwabEeCc/QUlEEWGkz+FBULEhGDiilJOcmkoICiiigCBTgyEelTCYKNuO1RqCByaCAB1P4mgqIzezcYNNZgRgGncKKjJ7msyiaEZxzT/K5zuqRHPlfN6UlaGYUU3zVzikP+rznoKAHFgO9JEncvUaOc4JpIRhhjsaDQd5pJwG/DFOEuSAf5Uu09d3PejZ3Y0GY6o6f8v3aZQAVJRTYxhcUANopqxbWJOaPLY80GhNgelFOQgLnvio/tEmeUFBmOzjnNNtyMktNn6mkNyQf9WKZAoDgY60ATiKIf3D+NKYh90NmlEQPbNIuc9elACNb+WM5zTITuhBySee9IWY96rkHcQKDQlgBzIBn2pDCx6pT7b7xHtUhOOTQZ8g3BDuQeMVXQndjn86tZ64qvz2NAchG+078nvU8Z+XrmmQDqaW2+89TLY0JAQDyKrVYoqQEX7opaRW469KfHLt4IogR1IXiOM8VIXPef9KJpPvgevFRlznBJ6etVbUsM55zRSQnmmwj5PxqgJIgAMGb8KMn1zSQd+aUjBwKAHQsRjOalqJeVxSx/IKAJKiyM4zT/M9qjExB/wBX+OaAHUmxfSlEhboaegOOnegB6xKBgORSrEAMb6aVIpKAGmMZzTqKKAETIFLSsuO9NQYH40GYpGRg0wjy/wClPqID999DQA5g3U1GLZSf9cefap6Y4289qDQ//9k=";

const LogoMark = () => (
  <img src={LA_GRAINE_LOGO} alt="La Graine" style={{ width: 40, height: 40, borderRadius: 10, objectFit: "cover" }} />
);

// ─── MOCK DATA ────────────────────────────────────────────────────────────────
const mockMatches = [
  { id: 1, type: "asso", name: "Association Terre Vivante", domain: "Environnement & Biodiversité", need: "Collecte de fonds", location: "Lyon, Auvergne-Rhône-Alpes", score: 94, tags: ["Terrain", "Don mensuel", "Face-à-face"] },
  { id: 2, type: "asso", name: "Les Bâtisseurs Solidaires", domain: "Insertion professionnelle", need: "Bénévolat & Don", location: "Bordeaux, Nouvelle-Aquitaine", score: 88, tags: ["Formation", "Accompagnement"] },
  { id: 3, type: "recruteur", name: "Entreprise Horizon SAS", domain: "Tech & Innovation", offer: "Mécénat de compétences", location: "Paris, Île-de-France", score: 91, tags: ["Dev", "Design", "Data"] },
  { id: 4, type: "recruteur", name: "Groupe Avenir Durable", domain: "BTP & Construction", offer: "Partenariat stratégique", location: "Nantes, Pays de la Loire", score: 85, tags: ["Logistique", "Finance"] },
];

const benefits = [
  { icon: <LeafIcon size={28} color={COLORS.sage} />, title: "Impact réel & mesurable", desc: "Chaque mission de collecte génère un impact concret, traçable et mesurable pour votre association et vos donateurs." },
  { icon: <HandshakeIcon size={28} color={COLORS.sage} />, title: "Recruteurs éprouvés sur le terrain", desc: "Tous nos recruteurs ont fait leurs preuves en collecte face-à-face. Pas d'algorithme — des professionnels sélectionnés pour leur expérience réelle." },
  { icon: <UsersIcon size={28} color={COLORS.sage} />, title: "Communauté engagée", desc: "Rejoignez un réseau actif de porteurs de projets et de professionnels qui partagent les mêmes valeurs." },
  { icon: <StarIcon size={28} color={COLORS.sage} />, title: "Profils vérifiés", desc: "Associations et recruteurs passent par un processus de validation pour garantir la qualité des échanges." },
];

// ─── DB SCHEMA (SQL) ──────────────────────────────────────────────────────────
const DB_SCHEMA = `-- =============================================
-- SCHÉMA BASE DE DONNÉES — Plateforme Asso/Recruteurs
-- PostgreSQL 15+
-- =============================================

-- ENUM Types
CREATE TYPE user_role AS ENUM ('association', 'recruteur', 'admin');
CREATE TYPE partnership_type AS ENUM ('benevole', 'mecentat_competences', 'don_financier', 'partenariat_strategique', 'sponsoring');
CREATE TYPE mission_status AS ENUM ('en_attente', 'active', 'terminee', 'annulee');

-- ─── USERS ───────────────────────────────────
CREATE TABLE users (
  id           UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email        VARCHAR(255) UNIQUE NOT NULL,
  password     VARCHAR(255) NOT NULL,          -- bcrypt hash
  role         user_role NOT NULL,
  is_verified  BOOLEAN DEFAULT FALSE,
  created_at   TIMESTAMPTZ DEFAULT NOW(),
  updated_at   TIMESTAMPTZ DEFAULT NOW()
);

-- ─── ASSOCIATIONS ────────────────────────────
CREATE TABLE associations (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id         UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  name            VARCHAR(255) NOT NULL,
  siret           VARCHAR(14),
  object_social   TEXT,
  domain          VARCHAR(100),               -- ex: Environnement, Education...
  description     TEXT,
  logo_url        VARCHAR(500),
  website         VARCHAR(500),
  created_year    SMALLINT,
  members_count   INTEGER,
  CONSTRAINT fk_user FOREIGN KEY (user_id) REFERENCES users(id)
);

-- ─── RECRUTEURS / ENTREPRISES ────────────────
CREATE TABLE recruteurs (
  id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id         UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  company_name    VARCHAR(255) NOT NULL,
  siret           VARCHAR(14),
  sector          VARCHAR(100),
  description     TEXT,
  logo_url        VARCHAR(500),
  website         VARCHAR(500),
  employee_count  INTEGER,
  csr_goals       TEXT,
  CONSTRAINT fk_user FOREIGN KEY (user_id) REFERENCES users(id)
);

-- ─── LOCALISATIONS ───────────────────────────
CREATE TABLE localizations (
  id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  entity_type VARCHAR(20) NOT NULL,            -- 'association' | 'recruteur'
  entity_id   UUID NOT NULL,
  address     VARCHAR(500),
  city        VARCHAR(100),
  department  VARCHAR(100),
  region      VARCHAR(100),
  postal_code VARCHAR(10),
  lat         DECIMAL(9,6),
  lng         DECIMAL(9,6)
);

-- ─── BESOINS / OFFRES ────────────────────────
CREATE TABLE partnership_needs (
  id               UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  association_id   UUID NOT NULL REFERENCES associations(id) ON DELETE CASCADE,
  type             partnership_type NOT NULL,
  title            VARCHAR(255),
  description      TEXT,
  skills_needed    TEXT[],                     -- ex: {Design, Marketing, RH}
  hours_per_week   SMALLINT,
  start_date       DATE,
  end_date         DATE,
  is_active        BOOLEAN DEFAULT TRUE,
  created_at       TIMESTAMPTZ DEFAULT NOW()
);

CREATE TABLE partnership_offers (
  id             UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  recruteur_id   UUID NOT NULL REFERENCES recruteurs(id) ON DELETE CASCADE,
  type           partnership_type NOT NULL,
  title          VARCHAR(255),
  description    TEXT,
  skills_offered TEXT[],
  hours_per_week SMALLINT,
  is_active      BOOLEAN DEFAULT TRUE,
  created_at     TIMESTAMPTZ DEFAULT NOW()
);

-- ─── MISE EN RELATION ────────────────────────
CREATE TABLE matches (
  id               UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  association_id   UUID NOT NULL REFERENCES associations(id),
  recruteur_id     UUID NOT NULL REFERENCES recruteurs(id),
  need_id          UUID REFERENCES partnership_needs(id),
  offer_id         UUID REFERENCES partnership_offers(id),
  score            SMALLINT,                   -- 0–100
  initiated_by     user_role,
  status           mission_status DEFAULT 'en_attente',
  message          TEXT,
  created_at       TIMESTAMPTZ DEFAULT NOW(),
  updated_at       TIMESTAMPTZ DEFAULT NOW()
);

-- ─── MESSAGES ────────────────────────────────
CREATE TABLE messages (
  id          UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  match_id    UUID NOT NULL REFERENCES matches(id) ON DELETE CASCADE,
  sender_id   UUID NOT NULL REFERENCES users(id),
  content     TEXT NOT NULL,
  read_at     TIMESTAMPTZ,
  created_at  TIMESTAMPTZ DEFAULT NOW()
);

-- ─── INDEXES ─────────────────────────────────
CREATE INDEX idx_asso_domain ON associations(domain);
CREATE INDEX idx_recruteur_sector ON recruteurs(sector);
CREATE INDEX idx_matches_asso ON matches(association_id);
CREATE INDEX idx_matches_recruteur ON matches(recruteur_id);
CREATE INDEX idx_localizations_entity ON localizations(entity_type, entity_id);
CREATE INDEX idx_needs_active ON partnership_needs(is_active) WHERE is_active = TRUE;
CREATE INDEX idx_offers_active ON partnership_offers(is_active) WHERE is_active = TRUE;

-- ─── UPDATED_AT TRIGGER ──────────────────────
CREATE OR REPLACE FUNCTION update_updated_at()
RETURNS TRIGGER AS $$
BEGIN NEW.updated_at = NOW(); RETURN NEW; END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER trg_users_updated_at BEFORE UPDATE ON users
  FOR EACH ROW EXECUTE FUNCTION update_updated_at();
CREATE TRIGGER trg_matches_updated_at BEFORE UPDATE ON matches
  FOR EACH ROW EXECUTE FUNCTION update_updated_at();`;

// ─── COMPONENTS ──────────────────────────────────────────────────────────────

// NAVBAR
function Navbar({ currentPage, setCurrentPage, user, setUser }) {
  const [scrolled, setScrolled] = useState(false);
  const [menuOpen, setMenuOpen] = useState(false);

  useEffect(() => {
    const onScroll = () => setScrolled(window.scrollY > 20);
    window.addEventListener("scroll", onScroll);
    return () => window.removeEventListener("scroll", onScroll);
  }, []);

  return (
    <nav style={{
      position: "fixed", top: 0, left: 0, right: 0, zIndex: 100,
      background: scrolled ? "rgba(245,240,232,0.92)" : "transparent",
      backdropFilter: scrolled ? "blur(16px)" : "none",
      borderBottom: scrolled ? "1px solid rgba(26,74,46,0.08)" : "none",
      transition: "all 0.3s ease",
      padding: "0 24px",
    }}>
      <div style={{ maxWidth: 1160, margin: "0 auto", height: 72, display: "flex", alignItems: "center", justifyContent: "space-between" }}>
        {/* Logo */}
        <button onClick={() => setCurrentPage("home")} style={{ display: "flex", alignItems: "center", gap: 12, background: "none", border: "none", cursor: "pointer" }}>
          <LogoMark />
          <span style={{ fontFamily: "'Playfair Display', serif", fontSize: 20, fontWeight: 700, color: COLORS.forest, letterSpacing: "-0.3px" }}>
            La <span style={{ color: COLORS.sage }}>Graine</span>
          </span>
        </button>

        {/* Desktop nav */}
        <div style={{ display: "flex", alignItems: "center", gap: 8 }}>
          {["home", "register", ...(user ? ["dashboard"] : [])].map(p => (
            <button key={p} className="btn-ghost"
              onClick={() => setCurrentPage(p)}
              style={{ color: currentPage === p ? COLORS.sage : undefined, fontWeight: currentPage === p ? "600" : "400" }}>
              {{ home: "Accueil", register: "S'inscrire", dashboard: "Dashboard" }[p]}
            </button>
          ))}
          {user ? (
            <div style={{ display: "flex", alignItems: "center", gap: 12, marginLeft: 8 }}>
              <div style={{ width: 36, height: 36, borderRadius: "50%", background: COLORS.forest, display: "flex", alignItems: "center", justifyContent: "center" }}>
                <span style={{ color: "white", fontSize: 13, fontWeight: 700 }}>{user.name?.[0] || "U"}</span>
              </div>
              <button className="btn-ghost" onClick={() => setUser(null)} style={{ fontSize: 13, color: "#888" }}>Déconnexion</button>
            </div>
          ) : (
            <button className="btn-primary" onClick={() => setCurrentPage("auth")} style={{ marginLeft: 8, padding: "10px 24px", fontSize: 14 }}>
              Connexion
            </button>
          )}
        </div>
      </div>
    </nav>
  );
}

// LANDING PAGE
function LandingPage({ setCurrentPage }) {
  return (
    <div>
      {/* HERO */}
      <section className="mesh-bg noise-overlay" style={{ minHeight: "100vh", display: "flex", alignItems: "center", paddingTop: 72 }}>
        <div style={{ maxWidth: 1160, margin: "0 auto", padding: "80px 24px", display: "flex", flexDirection: "column", alignItems: "center", textAlign: "center", maxWidth: 720, margin: "0 auto" }}>
          <div>
            <div className="animate-fadeUp" style={{ display: "inline-flex", alignItems: "center", gap: 8, background: "rgba(109,191,142,0.15)", border: "1px solid rgba(109,191,142,0.3)", borderRadius: 50, padding: "6px 16px", marginBottom: 28 }}>
              <div style={{ width: 7, height: 7, borderRadius: "50%", background: COLORS.mint, animation: "pulse 2s ease infinite" }} />
              <span style={{ fontSize: 12, fontWeight: 600, color: COLORS.sage, letterSpacing: "0.8px", textTransform: "uppercase" }}>Plateforme collaborative</span>
            </div>
            <h1 className="font-display animate-fadeUp delay-100" style={{ fontSize: "clamp(36px, 5vw, 60px)", fontWeight: 700, color: COLORS.forest, lineHeight: 1.1, marginBottom: 24 }}>
              Recruteurs &<br />Associations,<br /><em style={{ color: COLORS.sage, fontStyle: "italic" }}>ensemble</em>.
            </h1>
            <p className="animate-fadeUp delay-200" style={{ fontSize: 18, color: "#4a5e50", lineHeight: 1.7, marginBottom: 40, maxWidth: 600 }}>
              La Graine connecte les recruteurs de donateurs indépendants avec les associations partenaires — pour développer la philanthropie ensemble.
            </p>
            <div className="animate-fadeUp delay-300" style={{ display: "flex", gap: 14, flexWrap: "wrap" }}>
              <button className="btn-primary" onClick={() => setCurrentPage("register")} style={{ display: "flex", alignItems: "center", gap: 8 }}>
                S'inscrire ici <ArrowRightIcon size={16} color="currentColor" />
              </button>
              <button className="btn-outline" onClick={() => setCurrentPage("auth")}>
                Se connecter
              </button>
            </div>
          </div>


        </div>
      </section>

      {/* BENEFITS */}
      <section style={{ padding: "100px 24px", background: COLORS.mist }}>
        <div style={{ maxWidth: 1160, margin: "0 auto" }}>
          <div style={{ textAlign: "center", marginBottom: 64 }}>
            <h2 className="font-display" style={{ fontSize: 42, fontWeight: 700, color: COLORS.forest, marginBottom: 16 }}>
              Pourquoi choisir La Graine ?
            </h2>
            <p style={{ fontSize: 18, color: "#4a5e50", maxWidth: 560, margin: "0 auto" }}>
              Une plateforme pensée pour connecter des recruteurs expérimentés avec des associations qui ont besoin de développer leur base de donateurs.
            </p>
          </div>
          <div style={{ display: "grid", gridTemplateColumns: "repeat(2, 1fr)", gap: 28 }}>
            {benefits.map((b, i) => (
              <div key={i} className="card" style={{ padding: 36, display: "flex", gap: 24 }}>
                <div style={{ width: 60, height: 60, borderRadius: 16, background: `rgba(109,191,142,0.12)`, display: "flex", alignItems: "center", justifyContent: "center", flexShrink: 0 }}>
                  {b.icon}
                </div>
                <div>
                  <h3 style={{ fontSize: 18, fontWeight: 700, color: COLORS.forest, marginBottom: 10 }}>{b.title}</h3>
                  <p style={{ fontSize: 15, color: "#4a5e50", lineHeight: 1.7 }}>{b.desc}</p>
                </div>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* FOR WHOM */}
      <section style={{ padding: "100px 24px", background: COLORS.cream }}>
        <div style={{ maxWidth: 1160, margin: "0 auto", display: "grid", gridTemplateColumns: "1fr 1fr", gap: 40 }}>
          {[
            { role: "Recruteur de donateurs indépendant", color: COLORS.forest, bg: `linear-gradient(135deg, ${COLORS.forest}, ${COLORS.sage})`, items: ["Accédez à un réseau d'associations partenaires", "Gérez vos missions de collecte", "Suivez vos performances et donations", "Développez votre portefeuille de clients associatifs", "Valorisez votre impact terrain"] },
            { role: "Association partenaire", color: COLORS.sage, bg: `linear-gradient(135deg, ${COLORS.sage}, ${COLORS.mint})`, items: ["Trouvez des recruteurs qualifiés et engagés", "Développez votre base de donateurs", "Gérez vos campagnes de collecte", "Suivez les résultats en temps réel", "Fidélisez vos donateurs sur le long terme"] },
          ].map((section, i) => (
            <div key={i} className="card" style={{ overflow: "hidden" }}>
              <div style={{ background: section.bg, padding: "40px 36px 32px", position: "relative" }}>
                <div style={{ fontSize: 12, fontWeight: 700, letterSpacing: "1.2px", textTransform: "uppercase", color: "rgba(255,255,255,0.6)", marginBottom: 10 }}>Pour le</div>
                <h3 className="font-display" style={{ fontSize: 34, fontWeight: 700, color: "white" }}>{section.role}</h3>
              </div>
              <div style={{ padding: "32px 36px" }}>
                {section.items.map((item, j) => (
                  <div key={j} style={{ display: "flex", alignItems: "center", gap: 14, marginBottom: j < section.items.length - 1 ? 16 : 0 }}>
                    <div style={{ width: 26, height: 26, borderRadius: "50%", background: `rgba(109,191,142,0.15)`, display: "flex", alignItems: "center", justifyContent: "center", flexShrink: 0 }}>
                      <CheckIcon size={14} color={COLORS.sage} />
                    </div>
                    <span style={{ fontSize: 15, color: "#3a4e40" }}>{item}</span>
                  </div>
                ))}
                <button className="btn-primary" style={{ marginTop: 32, width: "100%" }} onClick={() => {}}>
                  Je suis une {section.role.toLowerCase()} →
                </button>
              </div>
            </div>
          ))}
        </div>
      </section>

      {/* CTA FOOTER */}
      <section style={{ background: COLORS.forest, padding: "80px 24px", textAlign: "center" }}>
        <div style={{ maxWidth: 640, margin: "0 auto" }}>
          <h2 className="font-display" style={{ fontSize: 42, fontWeight: 700, color: COLORS.cream, marginBottom: 20, lineHeight: 1.2 }}>
            Prêt à créer du<br /><em style={{ color: COLORS.mint }}>lien utile</em> ?
          </h2>
          <p style={{ fontSize: 18, color: "rgba(245,240,232,0.7)", marginBottom: 40 }}>
            Rejoignez une équipe jeune et dynamique centrée sur l'humain avant tout.
          </p>
          <button className="btn-primary" style={{ background: COLORS.mint, color: COLORS.forest, fontSize: 16, padding: "16px 48px" }} onClick={() => {}}>
            Créer mon compte gratuitement
          </button>
        </div>
      </section>
    </div>
  );
}

// AUTH PAGE
function AuthPage({ setCurrentPage, setUser }) {
  const [mode, setMode] = useState("login");
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");
  const [name, setName] = useState("");

  const handleSubmit = () => {
    setUser({ name: name || email.split("@")[0], email, role: "association" });
    setCurrentPage("dashboard");
  };

  return (
    <div className="mesh-bg" style={{ minHeight: "100vh", display: "flex", alignItems: "center", justifyContent: "center", padding: "100px 24px 40px" }}>
      <div className="card" style={{ width: "100%", maxWidth: 460, padding: 48 }}>
        <div style={{ textAlign: "center", marginBottom: 36 }}>
          <LogoMark />
          <h2 className="font-display" style={{ fontSize: 28, fontWeight: 700, color: COLORS.forest, marginTop: 16, marginBottom: 6 }}>
            {mode === "login" ? "Bon retour !" : "Rejoignez La Graine"}
          </h2>
          <p style={{ fontSize: 14, color: "#888" }}>
            {mode === "login" ? "Connectez-vous à votre espace" : "Créez votre compte en quelques minutes"}
          </p>
        </div>

        {/* Toggle */}
        <div style={{ display: "flex", background: COLORS.mist, borderRadius: 12, padding: 4, marginBottom: 32 }}>
          {["login", "signup"].map(m => (
            <button key={m} onClick={() => setMode(m)} style={{
              flex: 1, padding: "10px", borderRadius: 9, border: "none", cursor: "pointer", fontSize: 14, fontWeight: 600, fontFamily: "'DM Sans', sans-serif",
              background: mode === m ? "white" : "transparent",
              color: mode === m ? COLORS.forest : "#888",
              boxShadow: mode === m ? "0 2px 8px rgba(0,0,0,0.08)" : "none",
              transition: "all 0.2s",
            }}>
              {m === "login" ? "Connexion" : "Inscription"}
            </button>
          ))}
        </div>

        <div style={{ display: "flex", flexDirection: "column", gap: 20 }}>
          {mode === "signup" && (
            <div>
              <label className="label">Nom complet</label>
              <input className="input-field" placeholder="Marie Dupont" value={name} onChange={e => setName(e.target.value)} />
            </div>
          )}
          <div>
            <label className="label">Email</label>
            <input className="input-field" type="email" placeholder="marie@association.fr" value={email} onChange={e => setEmail(e.target.value)} />
          </div>
          <div>
            <label className="label">Mot de passe</label>
            <input className="input-field" type="password" placeholder="••••••••" value={password} onChange={e => setPassword(e.target.value)} />
          </div>
          <button className="btn-primary" style={{ width: "100%", marginTop: 8 }} onClick={handleSubmit}>
            {mode === "login" ? "Se connecter" : "Créer mon compte"}
          </button>
        </div>

        <p style={{ textAlign: "center", marginTop: 24, fontSize: 14, color: "#888" }}>
          {mode === "login" ? "Pas encore de compte ? " : "Déjà un compte ? "}
          <button onClick={() => setMode(mode === "login" ? "signup" : "login")} style={{ background: "none", border: "none", cursor: "pointer", color: COLORS.sage, fontWeight: 600, fontFamily: "inherit", fontSize: 14 }}>
            {mode === "login" ? "S'inscrire" : "Se connecter"}
          </button>
        </p>
      </div>
    </div>
  );
}

// MULTI-STEP REGISTRATION FORM
function RegisterPage({ setCurrentPage, setUser }) {
  const [profile, setProfile] = useState("association");
  const [step, setStep] = useState(1);
  const [formData, setFormData] = useState({});
  const totalSteps = profile === "recruteur" ? 3 : 4;

  const update = (key, val) => setFormData(prev => ({ ...prev, [key]: val }));

  const stepTitles = {
    association: ["Type de profil", "Votre association", "Vos besoins", "Récapitulatif"],
    recruteur: ["Type de profil", "Votre entreprise", "Vos offres", "Récapitulatif"],
  };

  const renderStep = () => {
    if (step === 1) return (
      <div className="animate-slideIn">
        <h3 className="font-display" style={{ fontSize: 24, color: COLORS.forest, marginBottom: 8 }}>Vous êtes…</h3>
        <p style={{ color: "#888", marginBottom: 32, fontSize: 15 }}>Choisissez votre profil pour personnaliser votre expérience.</p>
        <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 16 }}>
          {[
            { key: "recruteur", label: "Recruteur de donateurs indépendant", desc: "Je recrute des donateurs pour le compte d'associations partenaires.", icon: <HandshakeIcon size={32} color={profile === "recruteur" ? "white" : COLORS.sage} /> },
            { key: "association", label: "Association partenaire", desc: "Je recherche des recruteurs pour développer ma base de donateurs.", icon: <LeafIcon size={32} color={profile === "association" ? "white" : COLORS.sage} /> },
          ].map(p => (
            <button key={p.key} onClick={() => setProfile(p.key)} style={{
              padding: "28px 24px", borderRadius: 16, border: `2px solid ${profile === p.key ? COLORS.sage : COLORS.sand}`,
              background: profile === p.key ? `linear-gradient(135deg, ${COLORS.forest}, ${COLORS.sage})` : "white",
              cursor: "pointer", textAlign: "left", transition: "all 0.2s",
            }}>
              <div style={{ marginBottom: 14 }}>{p.icon}</div>
              <div style={{ fontSize: 16, fontWeight: 700, color: profile === p.key ? "white" : COLORS.forest, marginBottom: 8 }}>{p.label}</div>
              <div style={{ fontSize: 13, color: profile === p.key ? "rgba(255,255,255,0.75)" : "#888", lineHeight: 1.5 }}>{p.desc}</div>
            </button>
          ))}
        </div>
      </div>
    );

    if (step === 2 && profile === "association") return (
      <div className="animate-slideIn" style={{ display: "flex", flexDirection: "column", gap: 20 }}>
        <h3 className="font-display" style={{ fontSize: 24, color: COLORS.forest, marginBottom: 4 }}>Votre association</h3>
        <p style={{ color: "#888", fontSize: 15, marginBottom: 8 }}>Donnez de la visibilité à votre organisation.</p>
        <div>
          <label className="label">Nom de l'association *</label>
          <input className="input-field" placeholder="Ex : Les Jardins Solidaires" value={formData.name || ""} onChange={e => update("name", e.target.value)} />
        </div>
        <div>
          <label className="label">Objet social</label>
          <textarea className="input-field" rows={3} placeholder="Décrivez brièvement la mission de votre association…" style={{ resize: "vertical" }} value={formData.objet || ""} onChange={e => update("objet", e.target.value)} />
        </div>
        <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 16 }}>
          <div>
            <label className="label">Domaine d'activité</label>
            <select className="input-field" value={formData.domain || ""} onChange={e => update("domain", e.target.value)}>
              <option value="">Sélectionner…</option>
              {["Environnement", "Éducation", "Santé", "Insertion", "Sport", "Culture", "Humanitaire", "Autre"].map(d => <option key={d}>{d}</option>)}
            </select>
          </div>
          <div>
            <label className="label">Nombre de membres</label>
            <select className="input-field" value={formData.members || ""} onChange={e => update("members", e.target.value)}>
              <option value="">Sélectionner…</option>
              {["1–10", "11–50", "51–200", "200+"].map(m => <option key={m}>{m}</option>)}
            </select>
          </div>
        </div>
        <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 16 }}>
          <div>
            <label className="label">Ville *</label>
            <input className="input-field" placeholder="Lyon" value={formData.city || ""} onChange={e => update("city", e.target.value)} />
          </div>
          <div>
            <label className="label">Code postal</label>
            <input className="input-field" placeholder="69001" value={formData.postal || ""} onChange={e => update("postal", e.target.value)} />
          </div>
        </div>
      </div>
    );

    if (step === 2 && profile === "recruteur") return (
      <div className="animate-slideIn" style={{ display: "flex", flexDirection: "column", gap: 20 }}>
        <h3 className="font-display" style={{ fontSize: 24, color: COLORS.forest, marginBottom: 4 }}>Vos informations</h3>
        <p style={{ color: "#888", fontSize: 15, marginBottom: 8 }}>Quelques détails pour créer votre profil de recruteur indépendant.</p>
        <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 16 }}>
          <div>
            <label className="label">Prénom *</label>
            <input className="input-field" placeholder="Marie" value={formData.firstName || ""} onChange={e => update("firstName", e.target.value)} />
          </div>
          <div>
            <label className="label">Nom *</label>
            <input className="input-field" placeholder="Dupont" value={formData.lastName || ""} onChange={e => update("lastName", e.target.value)} />
          </div>
        </div>
        <div>
          <label className="label">Adresse e-mail *</label>
          <input className="input-field" type="email" placeholder="marie.dupont@email.com" value={formData.email || ""} onChange={e => update("email", e.target.value)} />
        </div>
        <div>
          <label className="label">Parlez-nous de vous</label>
          <textarea className="input-field" rows={4} placeholder="Décrivez brièvement votre parcours en collecte de fonds, vos expériences terrain, les associations avec lesquelles vous avez travaillé…" style={{ resize: "vertical" }} value={formData.bio || ""} onChange={e => update("bio", e.target.value)} />
        </div>
      </div>
    );

    if (step === 3 && profile === "association") return (
      <div className="animate-slideIn" style={{ display: "flex", flexDirection: "column", gap: 22 }}>
        <h3 className="font-display" style={{ fontSize: 24, color: COLORS.forest, marginBottom: 4 }}>Votre collecte</h3>
        <p style={{ color: "#888", fontSize: 15, marginBottom: 8 }}>Décrivez votre besoin en collecte de fonds face-à-face.</p>
        <div>
          <label className="label">Zones géographiques cibles</label>
          <input className="input-field" placeholder="Ex : Paris, Lyon, Bordeaux…" value={formData.zones || ""} onChange={e => update("zones", e.target.value)} />
        </div>
        <div>
          <label className="label">Objectif de la campagne</label>
          <textarea className="input-field" rows={3} placeholder="Décrivez votre campagne de collecte — projet financé, montant visé, durée…" style={{ resize: "vertical" }} value={formData.needDesc || ""} onChange={e => update("needDesc", e.target.value)} />
        </div>
        <div>
          <label className="label">Message aux recruteurs</label>
          <textarea className="input-field" rows={3} placeholder="Ce que vous attendez d'un recruteur de donateurs, vos valeurs, votre cause…" style={{ resize: "vertical" }} value={formData.message || ""} onChange={e => update("message", e.target.value)} />
        </div>
      </div>
    );

    if (step === 4) return (
      <div className="animate-slideIn" style={{ textAlign: "center" }}>
        <div style={{ width: 72, height: 72, borderRadius: "50%", background: `linear-gradient(135deg, ${COLORS.sage}, ${COLORS.mint})`, display: "flex", alignItems: "center", justifyContent: "center", margin: "0 auto 24px" }}>
          <CheckIcon size={32} color="white" />
        </div>
        <h3 className="font-display" style={{ fontSize: 26, color: COLORS.forest, marginBottom: 12 }}>Presque terminé !</h3>
        <p style={{ color: "#666", fontSize: 15, marginBottom: 36, lineHeight: 1.6 }}>
          Vérifiez votre saisie avant de finaliser votre inscription.
        </p>
        <div style={{ background: COLORS.mist, borderRadius: 16, padding: 28, textAlign: "left", marginBottom: 8 }}>
          {[
            ["Profil", profile === "association" ? "Association partenaire" : "Recruteur indépendant"],
            [profile === "association" ? "Nom de l'asso" : "Organisation", formData.name || formData.company || "—"],
            ["Ville", formData.city || "—"],
            profile === "association" ? ["Besoins", (formData.needs || []).join(", ") || "—"] : ["Offres", (formData.offers || []).join(", ") || "—"],
            ["Compétences", formData.skills || "—"],
          ].map(([k, v]) => (
            <div key={k} style={{ display: "flex", justifyContent: "space-between", padding: "10px 0", borderBottom: `1px solid ${COLORS.sand}` }}>
              <span style={{ fontSize: 13, color: "#888", fontWeight: 600, textTransform: "uppercase", letterSpacing: "0.3px" }}>{k}</span>
              <span style={{ fontSize: 14, color: COLORS.charcoal, fontWeight: 500, maxWidth: 200, textAlign: "right" }}>{v}</span>
            </div>
          ))}
        </div>
      </div>
    );
  };

  const handleFinish = () => {
    setUser({ name: formData.name || formData.company || "Mon Organisation", role: profile });
    setCurrentPage("dashboard");
  };

  return (
    <div className="mesh-bg" style={{ minHeight: "100vh", padding: "100px 24px 60px", display: "flex", alignItems: "flex-start", justifyContent: "center" }}>
      <div style={{ width: "100%", maxWidth: 580 }}>
        {/* Steps header */}
        <div style={{ marginBottom: 32 }}>
          <div style={{ display: "flex", justifyContent: "space-between", marginBottom: 10 }}>
            {stepTitles[profile].map((title, i) => (
              <div key={i} style={{ display: "flex", flexDirection: "column", alignItems: "center", flex: 1 }}>
                <div style={{ width: 32, height: 32, borderRadius: "50%", border: `2px solid ${i + 1 <= step ? COLORS.sage : COLORS.sand}`, background: i + 1 < step ? COLORS.sage : i + 1 === step ? "white" : "white", display: "flex", alignItems: "center", justifyContent: "center", transition: "all 0.3s", marginBottom: 6 }}>
                  {i + 1 < step ? <CheckIcon size={14} color="white" /> : <span style={{ fontSize: 12, fontWeight: 700, color: i + 1 === step ? COLORS.sage : COLORS.sand }}>{i + 1}</span>}
                </div>
                <span style={{ fontSize: 11, color: i + 1 === step ? COLORS.forest : "#aaa", fontWeight: i + 1 === step ? 600 : 400, textAlign: "center", lineHeight: 1.3 }}>{title}</span>
              </div>
            ))}
          </div>
          <div className="progress-bar" style={{ marginTop: 4 }}>
            <div className="progress-fill" style={{ width: `${(step / totalSteps) * 100}%` }} />
          </div>
        </div>

        <div className="card" style={{ padding: "40px 40px" }}>
          {renderStep()}
          <div style={{ display: "flex", justifyContent: "space-between", marginTop: 40, paddingTop: 24, borderTop: `1px solid ${COLORS.sand}` }}>
            <button className="btn-outline" onClick={() => step > 1 ? setStep(s => (profile === "recruteur" && s === 4) ? 2 : s - 1) : setCurrentPage("home")} style={{ padding: "12px 24px", fontSize: 14 }}>
              ← {step > 1 ? "Précédent" : "Accueil"}
            </button>
            {step < totalSteps ? (
              <button className="btn-primary" onClick={() => setStep(s => (profile === "recruteur" && s === 2) ? 4 : s + 1)} style={{ padding: "12px 28px" }}>
                Continuer →
              </button>
            ) : (
              <button className="btn-primary" onClick={handleFinish} style={{ background: COLORS.sage }}>
                Finaliser mon inscription ✓
              </button>
            )}
          </div>
        </div>
      </div>
    </div>
  );
}

// DASHBOARD
function Dashboard({ user, setCurrentPage }) {
  const [activeTab, setActiveTab] = useState("matches");
  const filtered = mockMatches.filter(m => user?.role === "association" ? m.type === "recruteur" : m.type === "asso");

  return (
    <div style={{ minHeight: "100vh", background: COLORS.mist, paddingTop: 72 }}>
      {/* Dashboard header */}
      <div style={{ background: COLORS.forest, padding: "40px 24px 60px" }}>
        <div style={{ maxWidth: 1160, margin: "0 auto" }}>
          <div style={{ display: "flex", alignItems: "center", gap: 20 }}>
            <div style={{ width: 60, height: 60, borderRadius: 18, background: `linear-gradient(135deg, ${COLORS.mint}, ${COLORS.sage})`, display: "flex", alignItems: "center", justifyContent: "center" }}>
              <span style={{ fontSize: 22, fontWeight: 800, color: "white" }}>{user?.name?.[0] || "U"}</span>
            </div>
            <div>
              <p style={{ fontSize: 13, color: "rgba(245,240,232,0.6)", letterSpacing: "0.5px", textTransform: "uppercase", fontWeight: 600 }}>Tableau de bord</p>
              <h2 className="font-display" style={{ fontSize: 28, fontWeight: 700, color: COLORS.cream }}>Bonjour, {user?.name || "Utilisateur"} 👋</h2>
            </div>
            <div style={{ marginLeft: "auto", display: "flex", gap: 10 }}>
              <span className="tag" style={{ background: user?.role === "association" ? "rgba(109,191,142,0.2)" : "rgba(200,168,75,0.2)", color: user?.role === "association" ? COLORS.mint : COLORS.gold, fontSize: 13 }}>
                {user?.role === "association" ? "🍃 Association partenaire" : "🤝 Recruteur indépendant"}
              </span>
            </div>
          </div>

        </div>
      </div>

      {/* Content */}
      <div style={{ maxWidth: 1160, margin: "-20px auto 0", padding: "0 24px 60px" }}>
        {/* Tabs */}
        <div style={{ display: "flex", gap: 4, background: "white", borderRadius: 16, padding: 6, marginBottom: 32, boxShadow: "0 2px 12px rgba(0,0,0,0.06)", width: "fit-content" }}>
          {[
            { key: "matches", label: "Suggestions" },
            { key: "messages", label: "Messages" },
            { key: "profile", label: "Mon profil" },
            { key: "schema", label: "Schéma BDD" },
          ].map(t => (
            <button key={t.key} onClick={() => setActiveTab(t.key)} style={{
              padding: "10px 22px", borderRadius: 11, border: "none", cursor: "pointer", fontSize: 14, fontWeight: 600, fontFamily: "'DM Sans', sans-serif",
              background: activeTab === t.key ? COLORS.forest : "transparent",
              color: activeTab === t.key ? "white" : "#888",
              transition: "all 0.2s",
            }}>{t.label}</button>
          ))}
        </div>

        {activeTab === "matches" && (
          <div>
            <h3 className="font-display" style={{ fontSize: 22, color: COLORS.forest, marginBottom: 20 }}>
              {user?.role === "association" ? "Recruteurs disponibles" : "Associations partenaires"}
            </h3>
            <div style={{ display: "grid", gridTemplateColumns: "repeat(2, 1fr)", gap: 20 }}>
              {filtered.map((m) => (
                <div key={m.id} className="card" style={{ padding: 28 }}>
                  <div style={{ display: "flex", justifyContent: "space-between", alignItems: "flex-start", marginBottom: 16 }}>
                    <div style={{ display: "flex", gap: 14, alignItems: "center" }}>
                      <div style={{ width: 46, height: 46, borderRadius: 13, background: `linear-gradient(135deg, ${m.type === "asso" ? COLORS.mint : COLORS.gold}, ${m.type === "asso" ? COLORS.sage : COLORS.forest})`, display: "flex", alignItems: "center", justifyContent: "center" }}>
                        {m.type === "asso" ? <LeafIcon size={20} color="white" /> : <HandshakeIcon size={20} color="white" />}
                      </div>
                      <div>
                        <div style={{ fontWeight: 700, color: COLORS.charcoal, fontSize: 15 }}>{m.name}</div>
                        <div style={{ fontSize: 12, color: "#888", marginTop: 2 }}>{m.domain}</div>
                      </div>
                    </div>
                    <div style={{ background: `rgba(109,191,142,0.12)`, borderRadius: 10, padding: "6px 12px", textAlign: "center" }}>
                      <div style={{ fontSize: 18, fontWeight: 800, color: COLORS.sage }}>{m.score}%</div>
                      <div style={{ fontSize: 10, color: "#888", textTransform: "uppercase", letterSpacing: "0.5px" }}>match</div>
                    </div>
                  </div>
                  <div style={{ display: "flex", alignItems: "center", gap: 6, marginBottom: 14 }}>
                    <MapPinIcon size={14} color="#aaa" />
                    <span style={{ fontSize: 13, color: "#888" }}>{m.location}</span>
                  </div>
                  <div style={{ display: "flex", gap: 6, flexWrap: "wrap", marginBottom: 18 }}>
                    {m.tags.map(t => <span key={t} className="tag" style={{ background: `rgba(26,74,46,0.07)`, color: COLORS.forest, fontSize: 11 }}>{t}</span>)}
                  </div>
                  <div style={{ fontSize: 13, color: "#666", background: COLORS.mist, borderRadius: 10, padding: "10px 14px", marginBottom: 16 }}>
                    <strong style={{ color: COLORS.forest }}>{m.type === "asso" ? m.need : m.offer}</strong>
                  </div>
                  <button className="btn-primary" style={{ width: "100%", padding: "12px", fontSize: 14 }}>
                    Contacter →
                  </button>
                </div>
              ))}
            </div>
          </div>
        )}

        {activeTab === "messages" && (
          <div style={{ display: "flex", gap: 20 }}>
            <div style={{ width: 300, background: "white", borderRadius: 16, padding: 20, boxShadow: "0 2px 12px rgba(0,0,0,0.06)" }}>
              <h4 style={{ color: COLORS.forest, marginBottom: 16, fontWeight: 700 }}>Conversations</h4>
              {[{ name: "Entreprise X", last: "Bonjour, nous serions…", time: "11h20", unread: 2 }, { name: "Groupe Avenir", last: "Merci pour votre intérêt.", time: "Hier" }].map((c, i) => (
                <div key={i} style={{ display: "flex", gap: 12, padding: "12px 0", borderBottom: i === 0 ? `1px solid ${COLORS.sand}` : "none", cursor: "pointer" }}>
                  <div style={{ width: 40, height: 40, borderRadius: "50%", background: COLORS.forest, display: "flex", alignItems: "center", justifyContent: "center", flexShrink: 0 }}>
                    <span style={{ color: "white", fontSize: 14, fontWeight: 700 }}>{c.name[0]}</span>
                  </div>
                  <div style={{ flex: 1, minWidth: 0 }}>
                    <div style={{ display: "flex", justifyContent: "space-between" }}>
                      <span style={{ fontWeight: 700, fontSize: 14, color: COLORS.forest }}>{c.name}</span>
                      <span style={{ fontSize: 11, color: "#aaa" }}>{c.time}</span>
                    </div>
                    <div style={{ fontSize: 12, color: "#888", overflow: "hidden", textOverflow: "ellipsis", whiteSpace: "nowrap" }}>{c.last}</div>
                  </div>
                  {c.unread && <div style={{ width: 20, height: 20, borderRadius: "50%", background: COLORS.mint, display: "flex", alignItems: "center", justifyContent: "center" }}><span style={{ fontSize: 10, color: "white", fontWeight: 700 }}>{c.unread}</span></div>}
                </div>
              ))}
            </div>
            <div style={{ flex: 1, background: "white", borderRadius: 16, padding: 32, boxShadow: "0 2px 12px rgba(0,0,0,0.06)", display: "flex", flexDirection: "column", alignItems: "center", justifyContent: "center" }}>
              <UsersIcon size={48} color={COLORS.sand} />
              <p style={{ color: "#aaa", marginTop: 16, fontSize: 15 }}>Sélectionnez une conversation</p>
            </div>
          </div>
        )}

        {activeTab === "profile" && (
          <div style={{ display: "grid", gridTemplateColumns: "1fr 2fr", gap: 24 }}>
            <div className="card" style={{ padding: 28, textAlign: "center" }}>
              <div style={{ width: 80, height: 80, borderRadius: "50%", background: `linear-gradient(135deg, ${COLORS.mint}, ${COLORS.forest})`, display: "flex", alignItems: "center", justifyContent: "center", margin: "0 auto 16px" }}>
                <span style={{ fontSize: 30, fontWeight: 800, color: "white" }}>{user?.name?.[0] || "U"}</span>
              </div>
              <h3 style={{ fontWeight: 700, fontSize: 18, color: COLORS.forest }}>{user?.name}</h3>
              <span className="tag" style={{ background: "rgba(109,191,142,0.12)", color: COLORS.sage, marginTop: 8, display: "inline-block" }}>
                {user?.role === "association" ? "Association partenaire" : "Recruteur indépendant"}
              </span>
              <div style={{ marginTop: 28 }}>
                <div style={{ marginBottom: 10 }}><div style={{ fontSize: 12, color: "#aaa", marginBottom: 4 }}>Profil complété</div><div className="progress-bar"><div className="progress-fill" style={{ width: "87%" }} /></div><div style={{ fontSize: 12, color: COLORS.sage, marginTop: 4, textAlign: "right" }}>87%</div></div>
              </div>
            </div>
            <div className="card" style={{ padding: 36 }}>
              <h3 style={{ fontWeight: 700, fontSize: 18, color: COLORS.forest, marginBottom: 24 }}>Modifier mon profil</h3>
              <div style={{ display: "grid", gridTemplateColumns: "1fr 1fr", gap: 18 }}>
                {[["Nom", user?.name, "name"], ["Email", "user@organisation.fr", "email"], ["Ville", "Paris", "city"], ["Téléphone", "+33 6 00 00 00 00", "phone"]].map(([l, v, k]) => (
                  <div key={k}>
                    <label className="label">{l}</label>
                    <input className="input-field" defaultValue={v} />
                  </div>
                ))}
              </div>
              <button className="btn-primary" style={{ marginTop: 24 }}>Sauvegarder les modifications</button>
            </div>
          </div>
        )}

        {activeTab === "schema" && (
          <div className="card" style={{ padding: 36 }}>
            <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 24 }}>
              <h3 className="font-display" style={{ fontSize: 22, color: COLORS.forest }}>Schéma Base de Données — PostgreSQL</h3>
              <span className="tag" style={{ background: "rgba(26,74,46,0.08)", color: COLORS.forest, fontSize: 12 }}>SQL</span>
            </div>
            <pre style={{ background: "#0d1117", color: "#c9d1d9", padding: "28px", borderRadius: 14, fontSize: 12, lineHeight: 1.7, overflow: "auto", maxHeight: 520, fontFamily: "'JetBrains Mono', 'Fira Code', monospace" }}>
              <code style={{ color: "#c9d1d9" }}>{DB_SCHEMA}</code>
            </pre>
          </div>
        )}
      </div>
    </div>
  );
}

// ─── FOLDER STRUCTURE MODAL ───────────────────────────────────────────────────
function FolderModal({ onClose }) {
  const tree = `la-graine/
├── 📁 frontend/          (React + Vite)
│   ├── public/
│   └── src/
│       ├── components/
│       │   ├── Navbar.jsx
│       │   ├── LandingPage.jsx
│       │   ├── RegisterForm.jsx  (multi-step)
│       │   ├── Dashboard.jsx
│       │   ├── AuthPage.jsx
│       │   └── ui/
│       │       ├── Button.jsx
│       │       ├── Input.jsx
│       │       └── Card.jsx
│       ├── pages/
│       │   ├── Home.jsx
│       │   ├── Auth.jsx
│       │   ├── Register.jsx
│       │   └── Dashboard.jsx
│       ├── hooks/
│       │   ├── useAuth.js
│       │   └── useMatches.js
│       ├── store/
│       │   └── authStore.js     (Zustand)
│       ├── api/
│       │   └── client.js        (axios)
│       ├── App.jsx
│       ├── main.jsx
│       └── index.css
│
├── 📁 backend/           (Node.js + Express)
│   ├── src/
│   │   ├── controllers/
│   │   │   ├── authController.js
│   │   │   ├── associationController.js
│   │   │   ├── recruteurController.js
│   │   │   └── matchController.js
│   │   ├── routes/
│   │   │   ├── auth.js
│   │   │   ├── associations.js
│   │   │   ├── recruteurs.js
│   │   │   └── matches.js
│   │   ├── middleware/
│   │   │   ├── auth.js          (JWT)
│   │   │   └── validate.js      (Zod)
│   │   ├── models/              (Sequelize/Prisma)
│   │   │   ├── User.js
│   │   │   ├── Association.js
│   │   │   ├── Recruteur.js
│   │   │   └── Match.js
│   │   ├── services/
│   │   │   └── matchingService.js
│   │   ├── config/
│   │   │   └── db.js
│   │   └── index.js
│   └── package.json
│
├── 📁 database/
│   ├── schema.sql
│   └── seed.sql
│
└── docker-compose.yml`;

  return (
    <div style={{ position: "fixed", inset: 0, zIndex: 200, background: "rgba(0,0,0,0.5)", display: "flex", alignItems: "center", justifyContent: "center", padding: 24 }} onClick={onClose}>
      <div className="card" style={{ maxWidth: 580, width: "100%", padding: 36, maxHeight: "80vh", overflow: "auto" }} onClick={e => e.stopPropagation()}>
        <div style={{ display: "flex", justifyContent: "space-between", alignItems: "center", marginBottom: 24 }}>
          <h3 className="font-display" style={{ fontSize: 22, color: COLORS.forest }}>Structure du projet</h3>
          <button onClick={onClose} style={{ background: COLORS.mist, border: "none", borderRadius: 8, padding: "6px 12px", cursor: "pointer", color: "#888" }}>✕</button>
        </div>
        <pre style={{ background: "#0d1117", color: "#c9d1d9", padding: 24, borderRadius: 12, fontSize: 12, lineHeight: 1.8, overflow: "auto", fontFamily: "'JetBrains Mono', monospace" }}>
          {tree}
        </pre>
      </div>
    </div>
  );
}

// ─── APP ──────────────────────────────────────────────────────────────────────
export default function App() {
  const [currentPage, setCurrentPage] = useState("home");
  const [user, setUser] = useState(null);
  const [showFolder, setShowFolder] = useState(false);

  return (
    <>
      <style>{globalStyles}</style>
      <Navbar currentPage={currentPage} setCurrentPage={setCurrentPage} user={user} setUser={setUser} />

      {currentPage === "home" && <LandingPage setCurrentPage={setCurrentPage} />}
      {currentPage === "auth" && <AuthPage setCurrentPage={setCurrentPage} setUser={setUser} />}
      {currentPage === "register" && <RegisterPage setCurrentPage={setCurrentPage} setUser={setUser} />}
      {currentPage === "dashboard" && <Dashboard user={user} setCurrentPage={setCurrentPage} />}

      {/* Floating folder structure button */}
      <button onClick={() => setShowFolder(true)} style={{
        position: "fixed", bottom: 24, right: 24, background: COLORS.forest, color: "white", border: "none", borderRadius: 14, padding: "12px 20px", cursor: "pointer", fontFamily: "'DM Sans', sans-serif", fontSize: 13, fontWeight: 600, boxShadow: "0 8px 24px rgba(26,74,46,0.3)", display: "flex", alignItems: "center", gap: 8, zIndex: 50,
      }}>
        📁 Structure du projet
      </button>

      {showFolder && <FolderModal onClose={() => setShowFolder(false)} />}
    </>
  );
}
