# Task Reviewer

Yazılım değişikliklerini ilk talebe göre bağımsız inceleyen bir Agent Skill. Web, mobil, masaüstü, backend, kütüphane ve altyapı projelerinde aynı inceleme akışını kullanır. Kontrolleri projenin kullandığı teknolojiye ve değişikliğin etkilediği davranışlara göre seçer. İnceleme sonunda bulguları ve doğrulama sınırlarını raporlar.

## Kurulum

[Hazır `task-reviewer.zip` dosyasını indir](https://github.com/dogukanyilmazel/task-reviewer/releases/latest/download/task-reviewer.zip).

| Araç | Kurulum | Kullanım |
| --- | --- | --- |
| [Codex](https://developers.openai.com/api/reference/cli#use-the-cli-from-a-coding-agent) | Tüm projeler için `task-reviewer/` klasörünü `~/.agents/skills/` altına kopyala. Projeye özel kullanım için proje kökündeki `.agents/skills/` altına kopyala. | `$task-reviewer` |
| [Claude Code](https://code.claude.com/docs/en/skills) | Tüm projeler için `task-reviewer/` klasörünü `~/.claude/skills/` altına kopyala. Projeye özel kullanım için `.claude/skills/` altına kopyala. | `/task-reviewer` |
| [Claude](https://support.claude.com/en/articles/12512180-use-skills-in-claude) | **Customize → Skills → + → Create skill → Upload a skill** üzerinden `task-reviewer.zip` dosyasını yükle. | Sohbette `task-reviewer` skill’ini kullanmasını iste. |
| [ChatGPT](https://help.openai.com/en/articles/20001066-skills-in-chatgpt) | Hesabında Skills varsa **Plugins → Skills → Create → Upload from your computer** üzerinden paketi yükle. Kullanılabilirlik hesap ve çalışma alanına bağlıdır. | Sohbette `task-reviewer` skill’ini kullanmasını iste. |
| Diğer AI araçları veya Skills menüsü olmayan hesaplar | Agent Skills desteği olan araçlarda klasörü aracın skill dizinine koy. Diğerlerinde `SKILL.md` dosyasını ekle veya metnini yapıştır. Gerekirse `references/review-lenses.md` dosyasını da ver. | İlk talebi ve incelenecek değişikliği gönder. |

## Örnek kullanım

> task-reviewer ile PR #42’yi incele. İlk isteğim, geçmiş tarihli bir kaydı içe aktardığımda kaydın geçmişte görünmesi ve güncel durum göstergesinin değişmemesiydi. Düzenleme ve silme sonrasında da güncel durumu kontrol et. Kodu değiştirmeden bulguları ve doğrulayamadığın noktaları yaz.

PR yerine bir commit, commit aralığı veya çalışma ağacındaki belirli dosyaları da verebilirsin. Sohbet aracı depoyu açamıyorsa ilk talebi, diff’i ve ilgili dosyaları ekle.

`REVIEW_PASS` mevcut kanıtın kabul için yeterli olduğunu, `CHANGES_REQUIRED` doğrulanmış bir sorunun düzeltilmesi gerektiğini, `REVIEW_INCONCLUSIVE` ise karar için önemli kanıtın eksik olduğunu belirtir.

## Projeye özgü inceleme notları

Tekrarlanan ürün kurallarını kendi projenin kökünde isteğe bağlı bir `REVIEW_CONTEXT.md` dosyasına yazabilirsin. Depoyu okuyamayan sohbet araçlarında bu dosyayı proje koduyla birlikte ekle veya ilgili kuralları mesajına yaz. Kuralı, etkilenen akışı ve kuralın doğrulanabileceği kodu, testi ya da belgeyi belirtmek yeterli.

```markdown
# Proje inceleme notları

- Güncel durum olay zamanına göre hesaplanır.
- Bir kayıt düzenlendiğinde veya silindiğinde özet ve bildirimler yeniden hesaplanır.
- Bu kuralların uygulandığı yerler ve kontroller: ilgili modül, test veya belge bağlantıları.
```
