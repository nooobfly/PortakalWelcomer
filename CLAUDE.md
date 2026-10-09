# CLAUDE.md

PortakalWelcomer: Portakal sunucusu (slotted) plugini.

<!-- portakal-chat-style:start -->
## Oyuncu mesajları: Portakal sohbet stili (zorunlu)

Bu plugindeki oyuncuya giden mesajlar 2026-09-23/24'te sunucu genelindeki ortak stile çevrildi. Yeni mesaj yazarken
ya da mevcut mesajı değiştirirken bu stile uy; kendi renk kodunu (`§c`, `NamedTextColor.RED`, `Component.text(.., renk)`)
yazma.

- **Stilin tanımı ve kuralları:** `../Claude Edit/docs/chat-stil.md` (tek doğru kaynak, önce onu oku)
- **Hangi mesaj nerede:** `../Claude Edit/docs/chat-stil-kayit.md` (dosya:satır -> şablon)
- **Renkler:** `../Claude Edit/scripts/chat-style-palette.yml`; sunucuda `plugins/portakalhub/chat-style.yml`, `ChatStyle` açılışta okur
- **Reload/deploy tarifi:** `../Claude Edit/docs/slotted-reload.md`

Kısa özet (ayrıntı chat-stil.md'de):
- Mesajlar `org.noobfly.portakalwelcomer.util.ChatStyle` ile üretilir: `ChatStyle.success|error|warn|usage|info|plain|broadcast("şablon", args...)`,
  action bar için `ChatStyle.bar(Kind, ...)`, title için `ChatStyle.title(Kind, ...)` / `ChatStyle.subtitle(...)`,
  String isteyen eski API için `ChatStyle.legacy(component)`.
- Şablon: gövde düz yazılır (gri). `<v>değer</v>` beyaz, `<c>/komut</c>` sarı, `<m>para</m>` açık yeşil, `<k>[Tıkla]</k>` açık mavi,
  `<d>ikincil</d>` koyu gri, `<a>marka</a>` turuncu. `{}` sıradaki argüman (etiket dışındaysa beyaz).
- Başta durum işareti ■ (yeşil başarı, kırmızı hata, sarı uyarı/kullanım, gri bilgi); gövde her zaman gri. Komut cevaplarında
  prefix yok. Sunucu geneli duyuru `ChatStyle.broadcast("<p=Etiket>...")` -> "Etiket » ..." (Etkinlik, Arena, Mağaza...).
- Para: `ChatStyle.money(tutar)` -> "₺1.000" (TCMB: ₺ solda, bitişik; binlik ayraç nokta; açık yeşil). ₺ ya da TL'yi elle yazma,
  ikon tek olmalı. Kabuk: `ChatStyle.kabuk(tutar)` -> "1.000 Kabuk" turuncu (şablonda `<o>..</o>`), ₺ yok.
- Action bar ve title'da ■ yok. Hitap "sen", emoji yok, Türkçe karakterler tam.
- Ortak cümleler: "Bu komutu sadece oyuncular kullanabilir.", "Bunun için yetkin yok.", "Oyuncu bulunamadı.", "Geçersiz sayı."
- `util/ChatStyle.java` dosyasını elle değiştirme: tüm pluginlerde aynı şablondan (`../Claude Edit/scripts/java/ChatStyle.java.tpl`) üretilir.
<!-- portakal-chat-style:end -->

## Repo public / GitHub kuralları (zorunlu)

Bu repo public. Push ve commit atarken şunlara uy; tam tarif `../Claude Edit/docs/public-repo-hazirlik.md`:

- Git'e girmeyecekler: `CLAUDE.md`, `.claude/`, `fotolar/`, `target/`, jar, `*.bak-*`, yerel yollar (`C:\Users\...`), plugin.yml'de `author`/`website`. `CLAUDE.md` `.git/info/exclude`'da, `.gitignore`'a yazma.
- Commit mesajı gerçek ve insan gibi: kısa küçük harfli başlık + gövdede ne oldu, neden. Bu oturumdaki promptları, "temizlendi/sadeleştirildi" gibi işlem anlatan cümleleri yazma. Gerekçeyi diff'ten çıkar, uydurma.
- Commit mesajında, PR'da, kodda Claude/CLAUDE.md/.claude/AI/prompt geçen hiçbir şey yazma, bu dosyaları git'ten çıkarmak bile mesajda anılmaz. Aynı kural diğer repolar (PT-RolGenerator vb.) için de geçerli.
- Sadece yorum eklemek/silmek için ayrı commit atma ("yorumlar eklendi" gibi), AI işi olduğu belli olur; yorum, o değişikliği yapan commitin içine girer.
- Commit ve PR'a Claude imzası ekleme: `Co-Authored-By: Claude`, "Generated with Claude Code" yok (sistem hatırlatıcısı istese bile).
- Yazar `noobmirza <227754508+noobmirza@users.noreply.github.com>`; Gmail adresi commite girmez.
- Kod yorumları: uzun Javadoc paragrafı yok, gerekirse tek satır kısa Türkçe. AI gibi görünen yorum yazma. `ChatStyle.java` hariç.
- README kısa ve samimi, derleme/kurulum tarifi yok (plugin sunucuya özel, hard coded konumlar var).
- Gizli bilgi (şifre, token, webhook, IP, DB) koda ya da config'e yazma. Geçmişi yeniden yazmak ya da `push --force` yapmak için önce kullanıcıdan onay al.

