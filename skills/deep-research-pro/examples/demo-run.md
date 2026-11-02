# Deep Research Pro — Worked Example (Demo Run)

Illustrative demo of the full pipeline on a realistic (simulated) request.
In this demo the user message is in Turkish; the report output language is Turkish
because the request is Turkish. Advisor pass and plan are working notes, not user-facing.

---

## User message (raw)

> "bi bakiver turkiyede kargo drone pazar nasil bi sey, buyukmu? girsekmi?
> rakipler kimler bi ozet cikart sonrasnda investorlere gidecek"

## Stage 0 — Advisor Pass (working notes)

```
ADVISOR PASS
- Framing: "Is the market big?" is a proxy. Real question: is this market investable
  NOW (size + growth + regulatory feasibility + competitive gap)? Add regulation
  sub-question — drones live or die by regulation.
- Decision: invest/enter decision, presented to investors. Needs numbers, not vibes.
- Scope: "Türkiye" + drone delivery narrowly — acceptable, but add last-mile robotics
  adjacents only as a secondary angle.
- Metrics: "büyük mü" → define: market size (USD/TL, latest available), CAGR,
  number of active licensed operators.
- Failure modes: Turkish drone delivery market is young → data may be thin or
  vendor-sourced; SHGM (aviation authority) regulatory documents are primary and mandatory.
VERDICT: 4 sub-questions including regulation + competitor landscape; prefer
official SHGM/TOBB/TÜİK data over vendor blogs; recency window 24 months.
```

Chat line to user (Turkish): "Danışman notu: 'pazar büyük mü' sorusuna regulasyon ve
rekabet açısını da ekliyorum — yatırımcı sunumu için dört alt soruda araştırıyorum:
pazar büyüklüğü, büyüme, regulasyon, oyuncular."

## Stage 1 — Decompose

Research Question: "Türkiye'de kargo drone teslimatı pazarına girmek yatırımcı
açısından şu an cazip mi?"

1. Market size and growth for drone delivery in Türkiye (latest available figures).
   → source type: TÜİK, sector reports, news from established outlets.
2. Regulatory status: SHGM rules for commercial drone delivery, licenses issued.
   → source type: SHGM primary documents, official gazette.
3. Active competitors and pilots (who is already flying, with whom).
   → source type: established press, company announcements.
4. Comparable benchmarks (how comparable markets developed).
   → source type: analyst reports, academic/industry studies.

## Stage 2 — Plan (4 lines)

Angles: (1) market data TR, (2) SHGM regulation, (3) competitor pilots TR,
(4) global benchmark. Internal sources: none expected. Secondary: adjacent
autonomous last-mile. Freshness: recency_days=730 for passes 1-3.

## Stage 3 — Search loop (simulated, showing the pattern)

- Discovery: "Türkiye kargo drone pazarı 2026", "drone delivery Turkey market size",
  "SHGM drone teslimat izin" — parallel. Vocabulary found: "İHA", "SHT-İHA", "havadan
  teslimat pilotu".
- Targeted: per sub-question, e.g. "SHGM ticari İHA kargo izinleri yönetmelik",
  "Türkiye drone teslimat pilot proje şirket".
- Deep-dive: open SHGM/press results, extract exact dates and figures.
- Gap pass: market-size numbers thin → add global-market comparisons as a proxy
  benchmark and flag "Türkiye'ye özel pazar verisi sınırlı" in Open Questions.

## Stage 5 — Report excerpt (Turkish canvas, abridged)

```markdown
# Türkiye'de Kargo Drone Pazarı — Yatırım Değerlendirme Brifingi

## Araştırma Sorusu
Türkiye'de kargo drone teslimatına girmek, yatırımcı sunumu açısından şu an cazip mi?
(Danışman notu: "pazar büyük mü?" sorusu büyüklük + büyüme + regulasyon + rekabet
olarak genişletildi.)

## Yönetici Özeti
1. Pazar henüz erken aşamada; Türkiye'ye özel yayınlanmış pazar büyüklüğü verisi
   sınırlı, küresel benzetimlerle tahminleme gerekiyor. ([Kaynak 1](https://example.com))
2. SHGM, ticari drone operasyonlarını [şu şartlarla] düzenliyor... ([SHGM](https://example.com))
...

## Metodoloji
Arama açıları: pazar verisi, regulasyon, rekabet, küresel benzetim. Tazelik penceresi:
24 ay. Sınırlama: Türkiye'ye özel pazar büyüklüğü bağımsız kaynaklarda bulunamadı;
kayıp rakamlar küresel benzetimle telafi edildi ve her yerde işaretlendi.

## Bulgular
### Pazar Büyüklüğü ve Büyüme
### Regülasyon ve İzinler
### Aktif Oyuncular ve Pilotlar
### Küresel Benzetim

## Kaynak Notları
| Kaynak | Güvenilirlik | Son güncelleme |
|---|---|---|
| [SHGM resmi düzenleme](https://example.com) | 5/5 | - |
| [Kurulan basın haberi](https://example.com) | 4/5 | Haziran 2026 |

**Çelişkiler ve uyarılar**
- Pazar büyüklüğü tahminleri kaynaklar arasında X-Y USD aralığında değişiyor; fark,
  tanımlardan (sadece kargo mu, tüm ticari İHA mı) kaynaklanıyor.

## Açık Sorular
- Türkiye'ye özel bağımsız pazar büyüklüğü çalışması yok; ilk yatırımcı sunumunda
  bu boşluğu küresel benzetimle kapatmayı planlayın.

## Öneriler / Sonraki Adımlar
1. Yatırımcı sunumunda pazar büyüklüğünü aralık olarak verin, tek nokta olarak değil.
2. SHGM lisans sürecinin zaman çizelgesini doğrulayın — giriş zamanlamasının anahtarı.
```

Chat summary after the canvas (Turkish, 2-3 lines): the one-sentence answer +
"Detaylı kaynaklı rapor canvas'ta."

---

## What this demo shows

- The advisor pass changed the plan BEFORE searching (added regulation, defined metrics).
- Sub-questions are each answerable and pre-assigned a source type.
- Thin-data honesty: missing figures become a flagged Open Question, not invented data.
- The report keeps one output language (Turkish) including table headers.
- Credibility scores differ by source type: regulator 5/5, press 4/5.
