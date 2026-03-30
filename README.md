<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <title>مصحفي الاحترافي</title>
    <link href="https://fonts.googleapis.com/css2?family=Amiri+Quran&family=Cairo:wght@400;700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Cairo', sans-serif; text-align: center; background: #f4f4f4; padding: 20px; }
        .card { background: white; padding: 20px; border-radius: 15px; box-shadow: 0 4px 8px rgba(0,0,0,0.1); max-width: 600px; margin: auto; }
        h1 { color: #0f4c3a; }
        p { font-family: 'Amiri Quran', serif; font-size: 1.5rem; line-height: 2; color: #333; }
    </style>
</head>
<body>
    <div class="card">
        <h1>القرآن الكريم</h1>
        <p>بِسْمِ اللَّهِ الرَّحْمَنِ الرَّحِيمِ <br> الحَمْدُ لِلَّهِ رَبِّ الْعَالَمِينَ ﴿١﴾ الرَّحْمَنِ الرَّحِيمِ ﴿٢﴾ مَالِكِ يَوْمِ الدِّينِ ﴿٣﴾</p>
        <hr>
        <small>تأكد من حفظ الملف بصيغة .html</small>
    </div>
</body>
</html>
const data = await res.json();
            const surah = data.data;
            
            surahTitle.textContent = surah.name;
            let fullText = '';
            
            // إضافة البسملة (إلا للفاتحة والتوبة)
            if (num != 1 && num != 9) {
                fullText += `<span class="basmalah">بِسْمِ ٱللَّهِ ٱلرَّحْمَٰنِ ٱلرَّحِيمِ</span>`;
            }

            surah.ayahs.forEach(ayah => {
                let text = ayah.text;
                // تنظيف البسملة من بداية الآية الأولى
                if (num != 1 && ayah.numberInSurah == 1) {
                    text = text.replace('بِسْمِ ٱللَّهِ ٱلرَّحْمَٰنِ ٱلرَّحِيمِ ', '');
                }
                const arNum = ayah.numberInSurah.toString().replace(/\d/g, d => '٠١٢٣٤٥٦٧٨٩'[d]);
                fullText += `${text} <span class="ayah-num">﴿${arNum}﴾</span> `;
            });

            quranContent.innerHTML = fullText;
            
            // تحديث الصوت
            const audioId = String(num).padStart(3, '0');
            mainAudio.src = `https://server8.mp3quran.net/afs/${audioId}.mp3`;
            
        } catch (err) {
            quranContent.innerHTML = 'حدث خطأ أثناء تحميل السورة.';
        }
        loading.style.display = 'none';
    }

    surahSelect.addEventListener('change', (e) => loadSurah(e.target.value));

    fetchSurahs();
</script>

</body>
</html>
