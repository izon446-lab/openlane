# Prompt Fixer — Worked Examples (Demo Runs)

Two demos: (A) explicit "fix my prompt" request, (B) a messy task executed silently.
Both are illustrative; outputs are abridged.

---

## Demo A — User asks for a prompt fix

**User message:**

> "yaw bi turlu anlatamadim kendimi, su promptu duzelt: 'rapor lazim satislar hakkinda
> bi seyler olsun gecen ay kiyas olsun guzel olsun yani patlamasin tablo filan'

**Step 1 — Extract intent:**
- Goal: a sales report comparing last month, safe for stakeholders, with a table.
- Context: "satışlar" → company sales data; no file specified → critical gap (which data?).
- Implicit expectation: "patlamasın" → nothing flashy/risky, no overstated claims;
  "güzel olsun" → presentable, polished. "Kıyas" → month-over-month comparison.

**Steps 2-3 — Corrected prompt (Turkish, since the user writes Turkish):**

```
GÖREV: Geçen ayın satış performansını önceki ayla karşılaştıran, yönetim
sunumuna uygun bir satış raporu hazırla.
BAĞLAM: [Satış verisi: hangi dosya/kaynak? — soruldu]
KAPSAM: Aylık toplam satış, ürün/kategori bazında kırılım, önceki aya göre
        değişim (adet ve ciro); dönem dışı veriler hariç.
KISITLAR: Ton profesyonel ve ölçülü; abartılı veya iddialı ifadeler yok
          ("patlamasın"); Türkçe; kısa yönetici özeti + tablo.
ÇIKTI: Canvas üzerinde rapor: 3-5 satırlık yönetici özeti + karşılaştırma
       tablosu + aylık trend grafiği.
BAŞARI ÖLÇÜTÜ: Sayılar doğru ve kaynağıyla eşleşiyor; yönetici özeti tek
               bakışta anlaşılıyor; iddialı yorum yok.
```

**Step 4 — Advisor pass:**

```
- "Hangi satış verisi?" belirtilmemiş → çalıştırılamaz. → KRİTİK: sorulacak.
  (Diğer her şey varsayımla kapanabilir; bu kapanamaz.)
- "Güzel olsun" ölçülebilir değil → başarı ölçütüne "tek bakışta anlaşılır özet +
  doğrulanabilir sayılar" olarak çevrildi. → Prompt güncellendi.
- Kategori kırılımı istenmedi ama kıyas raporu için gerekli → KAPSAM'a eklendi.
  [not sure: kırım ister misin söyle]
```

**User-facing reply (short):**

"Satış verisinin hangi dosyadan geleceğini belirtmen gerekiyor — onu sormadan
çalıştıramam. Gerisi tamam: patron sunumuna uygun, abartısız, tablolu bir kıyas
raporu prompt'u yazdım; kategori kırılımını ben ekledim, istemezsen çıkarırım.
Veriyi söyle, çalıştırayım."

---

## Demo B — Messy task, silent execution

**User message:**

> "eski musteriler icin bi win-back maili lazim 3-4 tane varyant bi de ilk mail
> konu satiri onemli cunku spam'e dusuyor"

**Step 1 — Extract intent:**
- Goal: win-back email for churned customers, 3-4 variants, with special attention to
  subject lines (spam-folder problem).
- Context: no company/offer details given → generic win-back structure with placeholders.
- Implicit expectation: variants must differ in angle (not just wording); subject lines
  must be spam-safe (avoid trigger words, caps, excessive punctuation).

**Step 2 — Gaps:** tone, offer details, company name — all placeholder-able, none critical.

**Step 3-4 — Internal prompt (not shown to user), advisor pass applied:**
- Advisor: "variants must differ in angle, not words" → explicit angle per variant
  (nostalgia/value/social-proof/urgency). "Spam" concern → add explicit subject-line rules.
- Advisor: no data on why customers left → mark assumption: generic churn, not
  complaint-driven churn.

**Step 5 — Execute directly.** User-facing message:

"Anladım: churn olmuş müşteriler için 3 farklı açıdan (nostalji/değer/itibar) win-back
maili + her biri için spam-safe konu satırı varyantları hazırlıyorum. Tek varsayım:
müşteriler şikayetten değil, sessizce uzaklaştığı için ayrılmış. Canvas geliyor."

Deliverable: canvas with the 3-4 variants, each with 2-3 subject-line options and a
one-line note on why the subject line is spam-safe.

---

## What these demos show

- Typos and fragments are read through, never corrected out loud.
- The deliverable constraint hidden in the last fragment ("investorlere gidecek" pattern)
  is caught and becomes an output constraint.
- Critical gaps (which data file) get asked; placeholder-able gaps (tone, offer) don't.
- The advisor pass changes the prompt before execution, and its fixes are visible in
  one line — not a wall of options.
- Messy task + no fix request = silent prompt, direct execution, one-line summary first.
