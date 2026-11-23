# Task Reviewer

Yazılım değişikliklerini ilk talebe göre bağımsız inceleyen bir Agent Skill. Web, mobil, masaüstü, backend, kütüphane ve altyapı projelerinde aynı inceleme akışını kullanır. Kontrolleri projenin kullandığı teknolojiye ve değişikliğin etkilediği davranışlara göre seçer. İnceleme sonunda bulguları ve doğrulama sınırlarını raporlar.

## Kurulum

| Araç | Kurulum | Kullanım |
| --- | --- | --- |
| [Codex](https://developers.openai.com/api/reference/cli#use-the-cli-from-a-coding-agent) | Tüm projeler için `task-reviewer/` klasörünü `~/.agents/skills/` altına kopyala. Projeye özel kullanım için proje kökündeki `.agents/skills/` altına kopyala. | `$task-reviewer` |
| [Claude Code](https://code.claude.com/docs/en/skills) | Tüm projeler için `task-reviewer/` klasörünü `~/.claude/skills/` altına kopyala. Projeye özel kullanım için `.claude/skills/` altına kopyala. | `/task-reviewer` |
| [Claude](https://support.claude.com/en/articles/12512180-use-skills-in-claude) | **Customize → Skills → + → Create skill → Upload a skill** üzerinden `task-reviewer.zip` dosyasını yükle. | Sohbette `task-reviewer` skill’ini kullanmasını iste. |
| [ChatGPT](https://help.openai.com/en/articles/20001066-skills-in-chatgpt) | Hesabında Skills varsa **Plugins → Skills → Create → Upload from your computer** üzerinden paketi yükle. Kullanılabilirlik hesap ve çalışma alanına bağlıdır. | Sohbette `task-reviewer` skill’ini kullanmasını iste. |
| Diğer AI araçları veya Skills menüsü olmayan hesaplar | Agent Skills desteği olan araçlarda klasörü aracın skill dizinine koy. Diğerlerinde `SKILL.md` dosyasını ekle veya metnini yapıştır. Gerekirse `references/review-lenses.md` dosyasını da ver. | İlk talebi ve incelenecek değişikliği gönder. |

ZIP dosyasını depodan üretmek için deponun kökünden `zip -r task-reviewer.zip task-reviewer -x '*/.DS_Store'` komutunu çalıştırabilirsin.

## Örnek kullanım

> task-reviewer ile son değişikliği ilk isteğime göre incele. İlgili kodu ve regresyonları kontrol et. Bulguları, dayandıkları kanıtı ve doğrulayamadığın noktaları yaz. Kodu değiştirme.

AI aracı projeyi doğrudan okuyabiliyorsa incelenecek PR’ı, commit’i veya çalışma ağacını belirt. Sohbet aracı projeyi okuyamıyorsa ilk isteği, diff’i ve ilgili dosyaları ekle. Skill’in inceleme kapsamı kendisine verdiğin kod ve araç erişimine bağlıdır.

`REVIEW_PASS` mevcut kanıtın kabul için yeterli olduğunu, `CHANGES_REQUIRED` doğrulanmış bir sorunun düzeltilmesi gerektiğini, `REVIEW_INCONCLUSIVE` ise karar için önemli kanıtın eksik olduğunu belirtir.
