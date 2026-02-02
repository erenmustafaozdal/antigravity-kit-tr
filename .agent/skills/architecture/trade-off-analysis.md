# Takas (Trade-off) Analizi ve ADR

> Her mimari kararı takaslarıyla (trade-offs) birlikte dökümante edin.

## Karar Çerçevesi

HER mimari bileşen için şunları dökümante edin:

```markdown
## Mimari Karar Kaydı (Architecture Decision Record - ADR)

### Bağlam (Context)
- **Sorun**: [Hangi sorunu çözüyoruz?]
- **Kısıtlamalar**: [Ekip boyutu, ölçek, zaman çizelgesi, bütçe]

### Değerlendirilen Seçenekler

| Seçenek | Artılar | Eksiler | Karmaşıklık | Ne Zaman Geçerli? |
|--------|------|------|------------|-----------|
| Seçenek A | Fayda 1 | Maliyet 1 | Düşük | [Koşullar] |
| Seçenek B | Fayda 2 | Maliyet 2 | Yüksek | [Koşullar] |

### Karar
**Seçilen**: [Seçenek B]

### Gerekçe
1. [Neden 1 - kısıtlamalarla bağlantılı]
2. [Neden 2 - gereksinimlerle bağlantılı]

### Kabul Edilen Takaslar (Trade-offs)
- [Nelerden feragat ediyoruz?]
- [Bu neden kabul edilebilir?]

### Sonuçlar
- **Pozitif**: [Kazandığımız faydalar]
- **Negatif**: [Kabul ettiğimiz maliyetler/riskler]
- **Azaltma (Mitigation)**: [Negatifleri nasıl yöneteceğiz?]

### Yeniden Değerlendirme Tetikleyicisi
- [Bu kararın ne zaman tekrar gözden geçirilmesi gerekir?]
```

## ADR Şablonu

```markdown
# ADR-[XXX]: [Karar Başlığı]

## Durum
Önerildi | Kabul Edildi | Kullanımdan Kaldırıldı | [ADR-YYY] ile Değiştirildi

## Bağlam (Context)
[Hangi sorun? Hangi kısıtlamalar?]

## Karar
[Neyi seçtik - spesifik olun]

## Gerekçe
[Neden seçtik - gereksinimlere ve kısıtlamalara bağlayın]

## Takaslar (Trade-offs)
[Nelerden vazgeçiyoruz - dürüst olun]

## Sonuçlar
- **Pozitif**: [Faydalar]
- **Negatif**: [Maliyetler]
- **Azaltma (Mitigation)**: [Nasıl çözüm üretilecek?]
```

## ADR Saklama Düzeni

```
docs/
└── architecture/
    ├── adr-001-nextjs-kullanimi.md
    ├── adr-002-mongodb-yerine-postgresql.md
    └── adr-003-repository-pattern-uygulanmasi.md
```
