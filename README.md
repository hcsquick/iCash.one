# iCash.one
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width,initial-scale=1"/>
<title>iCash.one Gateway Flow</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',Helvetica,Arial,sans-serif;font-size:14px;color:#172B4D;background:#F4F5F7;padding:20px}

/* ── Step nav bar ── */
.steps-bar{display:flex;align-items:stretch;background:white;border:1px solid #DFE1E6;border-radius:6px;overflow:hidden;margin-bottom:20px}
.sbar-item{flex:1;text-align:center;padding:10px 6px;font-size:11px;font-weight:600;color:#5E6C84;border-right:1px solid #DFE1E6;cursor:pointer;transition:background .15s;line-height:1.3}
.sbar-item:last-child{border-right:none}
.sbar-item.active{background:#0052CC;color:white}
.sbar-item:hover:not(.active){background:#F4F5F7}
.sbar-num{display:block;font-size:17px;font-weight:700;margin-bottom:2px}

/* ── Viewer layout ── */
.viewer{display:flex;gap:28px;align-items:flex-start}

/* ── Phone ── */
.phone-frame{width:230px;min-width:230px;background:white;border-radius:30px;border:3px solid #172B4D;box-shadow:0 8px 28px rgba(0,0,0,.18);overflow:hidden}
.phone-notch{height:22px;background:#172B4D;display:flex;align-items:center;justify-content:space-between;padding:0 14px}
.pn-dot{width:7px;height:7px;border-radius:50%;background:rgba(255,255,255,.3)}
.pn-bar{flex:1;height:3px;background:rgba(255,255,255,.2);border-radius:2px;margin:0 7px}
.phone-screen{min-height:370px;background:white;position:relative;overflow:hidden}
.slide{display:none;animation:fadeUp .22s ease}
.slide.active{display:block}
@keyframes fadeUp{from{opacity:0;transform:translateY(5px)}to{opacity:1;transform:translateY(0)}}

/* ── Screen chrome ── */
.s-header{padding:11px 15px 8px;display:flex;align-items:center;justify-content:space-between;border-bottom:1px solid #f0f0f0}
.s-exit{font-size:11px;color:#5E6C84}
.s-logo{font-size:13px;font-weight:800;color:#172B4D;letter-spacing:-.3px}
.s-logo em{color:#e53935;font-style:normal}
.s-body{padding:13px 15px}
.s-title{font-size:14px;font-weight:700;color:#172B4D;margin-bottom:5px;line-height:1.3}
.s-sub{font-size:10.5px;color:#5E6C84;margin-bottom:12px;line-height:1.4}
.s-label{font-size:10px;color:#5E6C84;font-weight:500;margin-bottom:3px}
.s-field{border:1.5px solid #DFE1E6;border-radius:5px;padding:7px 9px;font-size:11.5px;color:#172B4D;width:100%;background:#FAFBFC;margin-bottom:7px}
.s-btn{background:#e53935;color:white;border:none;border-radius:6px;padding:10px;font-size:12.5px;font-weight:700;width:100%;cursor:pointer;margin-top:4px}
.s-btn-ghost{background:none;border:none;color:#e53935;font-size:11.5px;font-weight:600;width:100%;padding:7px;cursor:pointer;text-align:center;display:block}
.s-methods{display:flex;gap:8px;margin-bottom:10px}
.s-method{border:1.5px solid #DFE1E6;border-radius:7px;padding:9px 7px;text-align:center;font-size:10px;font-weight:600;color:#344563;flex:1;cursor:pointer}
.s-method.sel{border-color:#0052CC;background:#DEEBFF;color:#0052CC}
.s-method-icon{font-size:17px;margin-bottom:2px}
.s-wallet-btn{background:#0052CC;color:white;border:none;border-radius:6px;padding:9px;font-size:12px;font-weight:600;width:100%;cursor:pointer;margin-bottom:8px}
.s-amount{background:#F4F5F7;border-radius:5px;padding:7px 10px;font-size:10.5px;color:#5E6C84;margin-top:8px}
.s-amount strong{color:#172B4D;font-size:12.5px;display:block;margin-top:1px}
.s-pay-to{display:flex;justify-content:space-between;font-size:10px;color:#5E6C84;margin-top:3px}
.s-pay-to span{color:#0052CC;font-weight:600}
.s-mpesa-badge{text-align:right;font-size:10px;font-weight:700;color:#00a651;margin-bottom:6px}
.s-row{display:flex;gap:7px}
.s-flag-box{border:1.5px solid #DFE1E6;border-radius:5px;padding:7px 9px;font-size:11px;background:#FAFBFC;display:flex;align-items:center;gap:4px;white-space:nowrap}
.s-voucher-input{border:2px solid #e53935;border-radius:7px;padding:10px;font-size:12px;color:#aaa;width:100%;text-align:center;letter-spacing:2px;margin-bottom:8px}
.s-get-it{display:flex;align-items:center;gap:8px;padding:6px 0}
.s-get-it p{font-size:10px;color:#5E6C84;flex:1;line-height:1.35}
.s-get-it-btn{background:#7c4dff;color:white;border:none;border-radius:5px;padding:6px 10px;font-size:10px;font-weight:700;cursor:pointer;white-space:nowrap}
.s-resellers{margin:4px 0 6px}
.s-reseller{display:flex;align-items:center;gap:8px;padding:6px 0;border-bottom:1px solid #f4f4f4;font-size:11px;color:#172B4D}
.s-reseller:last-child{border-bottom:none}
.s-reseller-icon{width:23px;height:23px;border-radius:5px;background:#f0f4ff;display:flex;align-items:center;justify-content:center;font-size:12px;flex-shrink:0}
.s-check{display:flex;align-items:flex-start;gap:7px;margin-bottom:11px}
.s-check-box{width:15px;height:15px;border-radius:3px;background:#0052CC;flex-shrink:0;display:flex;align-items:center;justify-content:center;margin-top:1px}
.s-check-text{font-size:10px;color:#344563;line-height:1.4}
.s-logo-big{text-align:center;font-size:20px;font-weight:900;color:#172B4D;margin-bottom:8px;letter-spacing:-.5px}
.s-logo-big em{color:#e53935;font-style:normal}

/* ── Description panel ── */
.desc{flex:1;min-width:0}
.desc-badge{display:inline-block;background:#0052CC;color:white;font-size:11px;font-weight:700;padding:2px 9px;border-radius:3px;margin-bottom:8px}
.desc-title{font-size:16px;font-weight:700;color:#172B4D;margin-bottom:10px;line-height:1.3}
.desc-body{font-size:13.5px;color:#344563;line-height:1.7;margin-bottom:12px}
.desc-note{background:white;border:1px solid #DFE1E6;border-left:3px solid #0065FF;border-radius:3px;padding:10px 13px;font-size:12.5px;color:#344563;margin-bottom:16px;line-height:1.55}
.desc-nav{display:flex;gap:8px}
.nav-btn{background:#0052CC;color:white;border:none;border-radius:4px;padding:8px 16px;font-size:13px;font-weight:600;cursor:pointer}
.nav-btn:hover{background:#0041a8}
.nav-btn.sec{background:white;color:#0052CC;border:1.5px solid #0052CC}
.nav-btn.sec:hover{background:#DEEBFF}
.nav-btn:disabled{background:#C1C7D0;border-color:#C1C7D0;cursor:not-allowed;color:white}
</style>
</head>
<body>

<!-- Step nav bar -->
<div class="steps-bar">
  <div class="sbar-item active" onclick="go(0)"><span class="sbar-num">1</span>Select method</div>
  <div class="sbar-item" onclick="go(1)"><span class="sbar-num">2A</span>Pay via M-Pesa</div>
  <div class="sbar-item" onclick="go(2)"><span class="sbar-num">2B</span>Enter voucher</div>
  <div class="sbar-item" onclick="go(3)"><span class="sbar-num">3</span>No voucher?</div>
  <div class="sbar-item" onclick="go(4)"><span class="sbar-num">4</span>Create account</div>
</div>

<!-- Viewer -->
<div class="viewer">

  <!-- Phone -->
  <div class="phone-frame">
    <div class="phone-notch">
      <div class="pn-dot"></div><div class="pn-bar"></div><div class="pn-dot"></div>
    </div>
    <div class="phone-screen">

      <!-- Slide 0: Select method -->
      <div class="slide active" id="s0">
        <div class="s-header"><div class="s-exit">← Exit</div><div class="s-logo">i<em>cash</em>.one</div></div>
        <div class="s-body">
          <div class="s-title">Payment Methods by iCash.One</div>
          <div class="s-sub">Select the payment method</div>
          <div class="s-methods">
            <div class="s-method"><div class="s-method-icon">🟢</div>M-Pesa</div>
            <div class="s-method sel"><div class="s-method-icon">🪙</div>iCash.One Voucher</div>
          </div>
          <button class="s-wallet-btn">iCash.One Wallet</button>
          <div class="s-amount">
            <div>Amount to pay</div>
            <strong>KES 500.00</strong>
            <div class="s-pay-to">Payment to <span>✓ Stake Global</span></div>
          </div>
        </div>
      </div>

      <!-- Slide 1: M-Pesa -->
      <div class="slide" id="s1">
        <div class="s-header"><div class="s-exit">← Exit</div><div class="s-logo">i<em>cash</em>.one</div></div>
        <div class="s-body">
          <div class="s-title">Complete your payment</div>
          <div class="s-mpesa-badge">M•PESA</div>
          <div class="s-label">Email</div>
          <div class="s-field">player@email.com</div>
          <div class="s-row">
            <div style="flex:0 0 76px">
              <div class="s-label">Country</div>
              <div class="s-flag-box">🇰🇪 254 ▾</div>
            </div>
            <div style="flex:1">
              <div class="s-label">Phone Number</div>
              <div class="s-field" style="margin:0">7XX XXX XXX</div>
            </div>
          </div>
          <div class="s-amount" style="margin-top:10px">
            <div>Amount to pay</div>
            <strong>KES 500.00</strong>
          </div>
          <button class="s-btn" style="margin-top:10px">Continue</button>
        </div>
      </div>

      <!-- Slide 2: Voucher code -->
      <div class="slide" id="s2">
        <div class="s-header"><div class="s-exit">← Exit</div><div class="s-logo">i<em>cash</em>.one</div></div>
        <div class="s-body">
          <div style="display:flex;align-items:center;gap:6px;margin-bottom:10px">
            <span style="color:#e53935;font-size:14px">🎟</span>
            <span style="font-size:13px;font-weight:700;color:#172B4D">Pay with iCash.One <span style="color:#e53935">Voucher</span></span>
          </div>
          <div style="font-size:11px;color:#5E6C84;margin-bottom:8px">Enter the voucher code</div>
          <div class="s-voucher-input">XXXX-XXXX-XXXX</div>
          <button class="s-btn">Pay</button>
          <div class="s-get-it">
            <p>Don't have a code?<br>Click to start & enjoy</p>
            <button class="s-get-it-btn">Get it here</button>
          </div>
          <div class="s-amount">
            <div>Amount to pay</div>
            <strong>KES 500.00</strong>
            <div class="s-pay-to">Payment to <span>✓ Stake Global</span></div>
          </div>
        </div>
      </div>

      <!-- Slide 3: Reseller list -->
      <div class="slide" id="s3">
        <div class="s-header"><div class="s-exit">← Exit</div><div class="s-logo">i<em>cash</em>.one</div></div>
        <div class="s-body">
          <div class="s-title" style="font-size:13px">Choose a verified Agent</div>
          <div style="font-size:10px;color:#5E6C84;margin-bottom:10px">Select from trusted distributors to buy a voucher</div>
          <div class="s-resellers">
            <div class="s-reseller"><div class="s-reseller-icon">💚</div>DM Pay</div>
            <div class="s-reseller"><div class="s-reseller-icon">📱</div>E-MPesa</div>
            <div class="s-reseller"><div class="s-reseller-icon">🎮</div>Baxity</div>
            <div class="s-reseller"><div class="s-reseller-icon">🦁</div>Moogold</div>
            <div class="s-reseller"><div class="s-reseller-icon">🎯</div>Offgamers</div>
            <div class="s-reseller"><div class="s-reseller-icon">⛏️</div>MINE Exchange</div>
          </div>
          <div style="font-size:10px;color:#5E6C84;text-align:center;margin-top:4px">List varies by country</div>
        </div>
      </div>

      <!-- Slide 4: Create account -->
      <div class="slide" id="s4">
        <div class="s-header"><div class="s-exit">← Exit</div><div class="s-logo">i<em>cash</em>.one</div></div>
        <div class="s-body">
          <div class="s-logo-big">i<em>cash</em>.one</div>
          <div class="s-title" style="font-size:13px;text-align:center">Create your iCash.One account for faster checkouts</div>
          <div class="s-sub" style="text-align:center;margin:8px 0 12px">To complete this payment securely, we'll use your email address to set up a free iCash account and send a temporary password to your inbox.</div>
          <div class="s-check">
            <div class="s-check-box"><span style="color:white;font-size:9px">✓</span></div>
            <div class="s-check-text">I agree to the creation of an iCash.One account and accept the Terms of Service and Privacy Policy</div>
          </div>
          <button class="s-btn">Continue</button>
          <button class="s-btn-ghost">Cancel payment</button>
        </div>
      </div>

    </div><!-- /phone-screen -->
  </div><!-- /phone-frame -->

  <!-- Description -->
  <div class="desc" id="desc"></div>

</div><!-- /viewer -->

<script>
const STEPS = [
  {
    badge: 'All markets — same UI',
    title: 'Step 1 — Select payment method',
    body: `When the player arrives at the iCash.one gateway from the Stake.com cashier, they see <strong>two payment methods</strong> and one wallet shortcut:<br><br>
    🟢 <strong>M-Pesa</strong> (or the local equivalent) — pay directly using phone number<br>
    🪙 <strong>iCash.One Voucher</strong> — enter a code already purchased from a reseller<br>
    💙 <strong>iCash.One Wallet</strong> — for players who already have a funded iCash.one account<br><br>
    The local payment method shown adapts automatically to the player's country.`,
    note: '💡 The local method shown (M-Pesa, UPI, MoMo, etc.) changes per market. The rest of the UI is identical everywhere.'
  },
  {
    badge: 'Path A — Direct local payment',
    title: 'Step 2A — Pay directly via M-Pesa (or local method)',
    body: `The player selects <strong>M-Pesa</strong> and provides:<br><br>
    • Their <strong>email address</strong><br>
    • Their <strong>country + phone number</strong><br><br>
    iCash.one triggers a payment request to their mobile wallet. The player approves on their phone and the Stake.com wallet is credited <strong>instantly</strong>.<br><br>
    If the player has no iCash.one account yet, one is created automatically using their email (see Step 4).`,
    note: '💡 Path A is the most frictionless for players in Kenya, Ghana, and Ivory Coast where mobile money is the primary financial tool.'
  },
  {
    badge: 'Path B — Existing voucher',
    title: 'Step 2B — Enter a voucher code',
    body: `The player already has an <strong>iCash.one voucher</strong> purchased from a reseller. They paste the code into the field and click <strong>Pay</strong>.<br><br>
    The gateway shows the amount (<em>e.g. KES 500.00</em>) and confirms the merchant as <strong>Stake Global</strong>.<br><br>
    Funds are deducted from the voucher instantly and the Stake.com wallet is credited — no further steps.<br><br>
    <strong>No voucher yet?</strong> → "Get it here" button takes them to the reseller list (next step).`,
    note: '💡 Voucher codes can be copied from the iCash.one portal or mobile app under "My Vouchers".'
  },
  {
    badge: 'No voucher → Reseller redirect',
    title: 'Step 3 — "Get it here" → Official reseller list',
    body: `If the player clicks <strong>"Get it here"</strong> inside the voucher screen, they are redirected to iCash.one's official <strong>verified reseller list</strong>, filtered by their country.<br><br>
    For Kenya this includes: DM Pay, E-MPesa, Baxity, Moogold, Offgamers, MINE Exchange, Ricko Agency, Bamboo Card, Deriv Add Pesa — each accepting different local methods.<br><br>
    The player:<br>
    1. Buys a voucher at a reseller using their preferred local method (M-Pesa, MoMo, UPI…)<br>
    2. Receives the code by email / on-screen<br>
    3. Returns to the gateway and enters the code`,
    note: '⚠️ Players should only use resellers from the official iCash.one list. Third-party sellers may provide invalid or already-used codes.'
  },
  {
    badge: 'Auto-triggered for new users',
    title: 'Step 4 — Create iCash.one account (first time only)',
    body: `If the player does not already have an iCash.one account, the gateway prompts them to create one after payment — <strong>one checkbox + Continue</strong>.<br><br>
    iCash.one sends a <strong>temporary password</strong> to their email for future access. No bank details or ID required — only an email address.<br><br>
    With an account the player can:<br>
    • View and manage vouchers<br>
    • Copy codes in one click<br>
    • Track transaction history<br>
    • Get expiry notifications<br><br>
    <strong>Returning players skip this step entirely</strong> — they are recognised by email and taken straight to checkout.`,
    note: '💡 This is a one-time step. All subsequent deposits on Stake.com via iCash.one will be faster since the account already exists.'
  }
];

let cur = 0;

function go(n) {
  cur = n;
  document.querySelectorAll('.slide').forEach((el, i) => el.classList.toggle('active', i === n));
  document.querySelectorAll('.sbar-item').forEach((el, i) => el.classList.toggle('active', i === n));
  const s = STEPS[n];
  document.getElementById('desc').innerHTML = `
    <div class="desc-badge">${s.badge}</div>
    <div class="desc-title">${s.title}</div>
    <div class="desc-body">${s.body}</div>
    <div class="desc-note">${s.note}</div>
    <div class="desc-nav">
      <button class="nav-btn sec" onclick="go(${n-1})" ${n===0?'disabled':''}>← Previous</button>
      <button class="nav-btn" onclick="go(${n+1})" ${n===STEPS.length-1?'disabled':''}>Next →</button>
    </div>`;
}
go(0);
</script>
</body>
</html>
