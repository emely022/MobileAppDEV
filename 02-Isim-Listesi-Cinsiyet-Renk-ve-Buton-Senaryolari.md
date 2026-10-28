# 👥 İsim Listesi + Yanında Okey Butonu / Checkbox / Switch ile Cinsiyete ve Duruma Göre Renk Değiştirme Senaryoları

> **[⬅️ Ana Sınav Rehberine (README) Dön](./README.md)**

![İsim Listesi ve Cinsiyete Göre Renk Değişimi Görsel Rehberi](./gorseller/02-isim-listesi-cinsiyet-renk.svg)

---

## 📌 Bu Dosya Hangi Hafta ve Hangi Ders Kodlarına Karşılık Gelir?

| Hafta | Ders Notu Dosyası ve Konu Başlığı | Hocanın Kodundaki Bileşen Adı | Ne İşe Yarar? |
| :--- | :--- | :--- | :--- |
| **Hafta 6 (W6)** | `W6 / components / FlatList.md` — **Example 1: Course Modules with Completion State** | `CourseModules` | Her satırın sağında bir `Switch` bulunur; onaylandığında (`done`) satırın arka planı yeşil (`#dcfce7`), kenarlığı `#22c55e` olur ve altta kaç tanesinin tamamlandığını (`Completed: X / Y`) yazar. |
| **Hafta 6 (W6)** | `W6 / components / Checkbox.md` — **Example 1: Lesson Task List** | `LessonChecklist` | Her satırın solunda `Checkbox` bulunur; işaretlendiğinde kutu rengi yeşil (`#22c55e`) olur ve yanındaki yazının üstü çizilir (`textDecorationLine: 'line-through'`). |
| **Hafta 6 (W6)** | `W6 / components / Checkbox.md` — **Example 2: Participant Settings Form** | `ParticipantSettings` | Satırların sağında `Checkbox` vardır; en az bir kutu seçildiğinde alttaki `Save Settings` butonu aktifleşir ve rengi maviye (`#38bdf8`) döner. |
| **Hafta 6 (W6)** | `W6 / components / TouchableOpacity.md` — **Example 1: Favorite Course Card** | `CourseCard` | Butona basıldıkça `isFavorite` state'ini tersine çevirir (`!prev`), butonun rengini (`#f59e0b` / `#334155`) ve üstündeki yazıyı değiştirir. |
| **Hafta 3 (W3)** | `W3 / 07-conditional-rendering-example.jsx` & `08-list-rendering-example.jsx` | `ConditionalList`, `TodoList` | `.map()` ve `.filter()` ile liste elemanlarını koşula göre farklı renk/ikon ve üstü çizili stille ekrana basar. |

---

## ⚡ Hoca Sınavda Renk veya Koşul Değiştirirse Hangi Kodu Değiştireceksin?

| Hocanın Görselde İstediği Değişiklik | Mantık / Formül | Kodda Değiştireceğin Yer |
| :--- | :--- | :--- |
| **Kadın ise Pembe, Erkek ise Mavi** (Sadece Okey verildiğinde) | `!isApproved ? '#ffffff' : item.gender === 'K' ? '#fce7f3' : '#dbeafe'` | Satırı saran `View` bileşeninin `backgroundColor` değeri |
| **Okey Butonunun Rengi** Cinsiyete Göre Değişsin | `!isApproved ? '#64748b' : item.gender === 'K' ? '#ec4899' : '#2563eb'` | `TouchableOpacity` bileşeninin `backgroundColor` değeri |
| **Okey Verilince Yazının Üstü Çizilsin** | `textDecorationLine: isApproved ? 'line-through' : 'none'` | İsim yazan `Text` bileşeninin `style` kısmı |
| **Buton İsmin Sağında Değil Solunda Olsun** | `<TouchableOpacity>...</TouchableOpacity>` bloğunu `<View>` (isim) bloğunun **üstüne** taşı | Satır içindeki `flexDirection: 'row'` düzeninde ilk yazılan solda, ikinci yazılan sağda görünür |
| **Buton İsmin Altında Olsun** | Satırın `flexDirection: 'row'` özelliğini `'column'` yap | Satırı saran `rowCard` stilindeki `flexDirection` değeri |
| **Sadece Kadınları veya Sadece Erkekleri Göster** | `PEOPLE.filter(p => filter === 'ALL' \|\| p.gender === filter)` | Listeye verilen `data` dizisini `.filter()` ile süz |

---

## 1️⃣ DERSTEKİ ÖZEL ÖRNEK (SENARYO 2A) — İsimlerin Yanında "Okey" Butonu: Okey Verdikçe İsmin Cinsiyetine Göre Renk Değiştirme

* **İlgili Ders Konusu:** Hafta 6 (`W6 / FlatList.md` — `CourseModules` + `W6 / TouchableOpacity.md` + `W6 / Checkbox.md`)
* **Bu Kod Ne İşe Yarar?**
  * Ekranda kadın (`gender: 'K'`) ve erkek (`gender: 'E'`) isimlerinden oluşan bir liste vardır.
  * Her ismin sağ tarafında bir **"Okey Ver"** butonu bulunur.
  * Bir ismin yanındaki butona tıkladığında (`toggleApprove(item.id)`):
    * Eğer kişi **Kadın (`K`)** ise: Kartın arka planı açık pembe (`#fce7f3`), çerçevesi koyu pembe (`#ec4899`), isim rengi bordo/pembe (`#9d174d`) ve butonun kendisi pembe (`#ec4899`) olup yazısı **"Okey ✓"** olur.
    * Eğer kişi **Erkek (`E`)** ise: Kartın arka planı açık mavi (`#dbeafe`), çerçevesi koyu mavi (`#2563eb`), isim rengi lacivert (`#1e40af`) ve butonun kendisi mavi (`#2563eb`) olup yazısı **"Okey ✓"** olur.
    * Tekrar tıklarsan onay kalkar ve kart tekrar nötr beyaz (`#ffffff`), buton ise gri (`#64748b`) rengine döner.
  * Ekranın altında toplam kaç kişiye (ve kaç kadın / kaç erkeğe) okey verildiğini canlı olarak sayar.

```jsx
import React, { useState } from 'react';
import { SafeAreaView, FlatList, View, Text, TouchableOpacity, StyleSheet } from 'react-native';

const PEOPLE = [
  { id: '1', name: 'Ayşe Yılmaz', gender: 'K' },
  { id: '2', name: 'Ahmet Demir', gender: 'E' },
  { id: '3', name: 'Zeynep Kaya', gender: 'K' },
  { id: '4', name: 'Mehmet Çelik', gender: 'E' },
  { id: '5', name: 'Elif Şahin', gender: 'K' },
  { id: '6', name: 'Can Arslan', gender: 'E' },
];

export default function GenderColorApprovalList() {
  const [approved, setApproved] = useState({});

  const toggleApprove = (id) => {
    setApproved((prev) => ({
      ...prev,
      [id]: !prev[id],
    }));
  };

  const approveAll = () => {
    const all = {};
    PEOPLE.forEach((person) => {
      all[person.id] = true;
    });
    setApproved(all);
  };

  const resetAll = () => {
    setApproved({});
  };

  const approvedCount = Object.values(approved).filter(Boolean).length;
  const approvedFemaleCount = PEOPLE.filter((p) => p.gender === 'K' && approved[p.id]).length;
  const approvedMaleCount = PEOPLE.filter((p) => p.gender === 'E' && approved[p.id]).length;

  return (
    <SafeAreaView style={styles.safeArea}>
      <View style={styles.container}>
        <Text style={styles.title}>Katılımcı Onay Listesi</Text>
        <Text style={styles.subtitle}>
          Okey verilen isimler cinsiyetine göre (Kadın: Pembe, Erkek: Mavi) renk değiştirir
        </Text>

        <View style={styles.topActions}>
          <TouchableOpacity style={styles.approveAllButton} onPress={approveAll}>
            <Text style={styles.topButtonText}>Tümüne Okey Ver</Text>
          </TouchableOpacity>
          <TouchableOpacity style={styles.resetButton} onPress={resetAll}>
            <Text style={styles.topButtonText}>Sıfırla</Text>
          </TouchableOpacity>
        </View>

        <FlatList
          data={PEOPLE}
          keyExtractor={(item) => item.id}
          contentContainerStyle={styles.listContent}
          renderItem={({ item }) => {
            const isApproved = !!approved[item.id];
            const isFemale = item.gender === 'K';

            const cardBg = !isApproved
              ? '#ffffff'
              : isFemale
              ? '#fce7f3'
              : '#dbeafe';

            const cardBorder = !isApproved
              ? '#cbd5e1'
              : isFemale
              ? '#ec4899'
              : '#2563eb';

            const nameColor = !isApproved
              ? '#1e293b'
              : isFemale
              ? '#9d174d'
              : '#1e40af';

            const buttonBg = !isApproved
              ? '#64748b'
              : isFemale
              ? '#ec4899'
              : '#2563eb';

            return (
              <View
                style={[
                  styles.rowCard,
                  { backgroundColor: cardBg, borderColor: cardBorder },
                ]}
              >
                <View style={styles.infoArea}>
                  <Text style={[styles.nameText, { color: nameColor }]}>
                    {item.name}
                  </Text>
                  <Text style={styles.genderText}>
                    Cinsiyet: {isFemale ? 'Kadın' : 'Erkek'} · Durum:{' '}
                    {isApproved ? 'Onaylandı' : 'Bekliyor'}
                  </Text>
                </View>

                <TouchableOpacity
                  style={[styles.okeyButton, { backgroundColor: buttonBg }]}
                  onPress={() => toggleApprove(item.id)}
                  activeOpacity={0.75}
                >
                  <Text style={styles.okeyButtonText}>
                    {isApproved ? 'Okey ✓' : 'Okey Ver'}
                  </Text>
                </TouchableOpacity>
              </View>
            );
          }}
        />

        <View style={styles.footerBox}>
          <Text style={styles.footerTitle}>
            Toplam Onaylanan: {approvedCount} / {PEOPLE.length}
          </Text>
          <Text style={styles.footerDetail}>
            Kadın: {approvedFemaleCount} · Erkek: {approvedMaleCount}
          </Text>
        </View>
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  safeArea: {
    flex: 1,
    backgroundColor: '#f8fafc',
  },
  container: {
    flex: 1,
    padding: 20,
  },
  title: {
    fontSize: 22,
    fontWeight: 'bold',
    color: '#0f172a',
    textAlign: 'center',
    marginBottom: 6,
  },
  subtitle: {
    fontSize: 13,
    color: '#475569',
    textAlign: 'center',
    marginBottom: 16,
  },
  topActions: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    gap: 12,
    marginBottom: 16,
  },
  approveAllButton: {
    flex: 1,
    backgroundColor: '#16a34a',
    paddingVertical: 12,
    borderRadius: 10,
    alignItems: 'center',
  },
  resetButton: {
    flex: 1,
    backgroundColor: '#dc2626',
    paddingVertical: 12,
    borderRadius: 10,
    alignItems: 'center',
  },
  topButtonText: {
    color: '#ffffff',
    fontWeight: 'bold',
    fontSize: 14,
  },
  listContent: {
    gap: 12,
    paddingBottom: 16,
  },
  rowCard: {
    flexDirection: 'row',
    alignItems: 'center',
    justifyContent: 'space-between',
    padding: 16,
    borderRadius: 14,
    borderWidth: 2,
  },
  infoArea: {
    flex: 1,
    marginRight: 12,
  },
  nameText: {
    fontSize: 17,
    fontWeight: 'bold',
    marginBottom: 4,
  },
  genderText: {
    fontSize: 13,
    color: '#64748b',
  },
  okeyButton: {
    paddingVertical: 10,
    paddingHorizontal: 18,
    borderRadius: 10,
    minWidth: 95,
    alignItems: 'center',
  },
  okeyButtonText: {
    color: '#ffffff',
    fontSize: 14,
    fontWeight: 'bold',
  },
  footerBox: {
    backgroundColor: '#0f172a',
    padding: 14,
    borderRadius: 12,
    alignItems: 'center',
    marginTop: 8,
  },
  footerTitle: {
    color: '#f8fafc',
    fontSize: 16,
    fontWeight: 'bold',
  },
  footerDetail: {
    color: '#38bdf8',
    fontSize: 13,
    marginTop: 4,
  },
});
```

---

## 2️⃣ SINAV SENARYOSU 2B — Yeni İsim ve Cinsiyet Ekleme + Filtreleme + Okey Verdikçe Cinsiyete Göre Renk Değişimi

* **İlgili Ders Konusu:** Hafta 4 (`SimpleForm`, `TextInputExample`) + Hafta 6 (`FlatList`, `TouchableOpacity`, `TextInput`)
* **Bu Kod Ne İşe Yarar?**
  * Hoca sınavda *"Listeye yeni bir isim ve cinsiyet ekleyebileceğiniz bir kutu koyun, eklenen ismin yanındaki Okey butonuna basınca da cinsiyetine göre pembe veya mavi olsun"* derse doğrudan bu kodu kullanabilirsin!
  * Üstte `TextInput` ile yeni isim yazılır, yanındaki **Kadın / Erkek** seçim butonlarından biri seçilir ve **Listeye Ekle** butonuna basılır.
  * Ayrıca **Tümü / Kadınlar / Erkekler** filtre butonlarıyla listeyi filtreleyebilirsin.

```jsx
import React, { useState } from 'react';
import {
  SafeAreaView,
  View,
  Text,
  TextInput,
  TouchableOpacity,
  FlatList,
  StyleSheet,
} from 'react-native';

const INITIAL_PEOPLE = [
  { id: '1', name: 'Ayşe Yılmaz', gender: 'K', approved: true },
  { id: '2', name: 'Ahmet Demir', gender: 'E', approved: true },
  { id: '3', name: 'Zeynep Kaya', gender: 'K', approved: false },
  { id: '4', name: 'Mehmet Çelik', gender: 'E', approved: false },
];

export default function AddPersonGenderColorList() {
  const [people, setPeople] = useState(INITIAL_PEOPLE);
  const [newName, setNewName] = useState('');
  const [selectedGender, setSelectedGender] = useState('K');
  const [filterGender, setFilterGender] = useState('ALL');

  const handleAddPerson = () => {
    if (newName.trim() === '') return;
    const newPerson = {
      id: String(Date.now()),
      name: newName.trim(),
      gender: selectedGender,
      approved: false,
    };
    setPeople((prev) => [...prev, newPerson]);
    setNewName('');
  };

  const togglePersonApprove = (id) => {
    setPeople((prev) =>
      prev.map((person) =>
        person.id === id ? { ...person, approved: !person.approved } : person
      )
    );
  };

  const filteredPeople = people.filter((person) => {
    if (filterGender === 'ALL') return true;
    return person.gender === filterGender;
  });

  return (
    <SafeAreaView style={styles.safeArea}>
      <View style={styles.container}>
        <Text style={styles.header}>İsim Ekleme ve Cinsiyet Renkli Onay</Text>

        <View style={styles.formCard}>
          <TextInput
            style={styles.input}
            placeholder="Yeni isim giriniz..."
            value={newName}
            onChangeText={setNewName}
          />

          <View style={styles.genderSelectRow}>
            <TouchableOpacity
              style={[
                styles.genderOption,
                selectedGender === 'K' && styles.femaleActiveOption,
              ]}
              onPress={() => setSelectedGender('K')}
            >
              <Text
                style={[
                  styles.genderOptionText,
                  selectedGender === 'K' && styles.activeOptionText,
                ]}
              >
                Kadın
              </Text>
            </TouchableOpacity>

            <TouchableOpacity
              style={[
                styles.genderOption,
                selectedGender === 'E' && styles.maleActiveOption,
              ]}
              onPress={() => setSelectedGender('E')}
            >
              <Text
                style={[
                  styles.genderOptionText,
                  selectedGender === 'E' && styles.activeOptionText,
                ]}
              >
                Erkek
              </Text>
            </TouchableOpacity>

            <TouchableOpacity style={styles.addButton} onPress={handleAddPerson}>
              <Text style={styles.addButtonText}>+ Ekle</Text>
            </TouchableOpacity>
          </View>
        </View>

        <View style={styles.filterRow}>
          {[
            { key: 'ALL', label: 'Tümü' },
            { key: 'K', label: 'Kadınlar' },
            { key: 'E', label: 'Erkekler' },
          ].map((tab) => (
            <TouchableOpacity
              key={tab.key}
              style={[
                styles.filterButton,
                filterGender === tab.key && styles.activeFilterButton,
              ]}
              onPress={() => setFilterGender(tab.key)}
            >
              <Text
                style={[
                  styles.filterText,
                  filterGender === tab.key && styles.activeFilterText,
                ]}
              >
                {tab.label}
              </Text>
            </TouchableOpacity>
          ))}
        </View>

        <FlatList
          data={filteredPeople}
          keyExtractor={(item) => item.id}
          contentContainerStyle={styles.listGap}
          renderItem={({ item }) => {
            const isFemale = item.gender === 'K';
            const bg = !item.approved
              ? '#ffffff'
              : isFemale
              ? '#fce7f3'
              : '#dbeafe';
            const border = !item.approved
              ? '#e2e8f0'
              : isFemale
              ? '#ec4899'
              : '#2563eb';
            const btnColor = !item.approved
              ? '#64748b'
              : isFemale
              ? '#ec4899'
              : '#2563eb';

            return (
              <View style={[styles.itemRow, { backgroundColor: bg, borderColor: border }]}>
                <View>
                  <Text style={styles.itemName}>{item.name}</Text>
                  <Text style={styles.itemSub}>
                    {isFemale ? 'Kadın' : 'Erkek'} · {item.approved ? 'Onaylı' : 'Onaysız'}
                  </Text>
                </View>

                <TouchableOpacity
                  style={[styles.okeyBtn, { backgroundColor: btnColor }]}
                  onPress={() => togglePersonApprove(item.id)}
                >
                  <Text style={styles.okeyBtnText}>
                    {item.approved ? 'Okey ✓' : 'Okey'}
                  </Text>
                </TouchableOpacity>
              </View>
            );
          }}
        />
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  safeArea: {
    flex: 1,
    backgroundColor: '#f1f5f9',
  },
  container: {
    flex: 1,
    padding: 18,
  },
  header: {
    fontSize: 20,
    fontWeight: 'bold',
    color: '#0f172a',
    textAlign: 'center',
    marginBottom: 12,
  },
  formCard: {
    backgroundColor: '#ffffff',
    padding: 14,
    borderRadius: 14,
    marginBottom: 14,
    gap: 10,
  },
  input: {
    borderWidth: 1,
    borderColor: '#cbd5e1',
    borderRadius: 10,
    paddingHorizontal: 12,
    paddingVertical: 10,
    fontSize: 15,
  },
  genderSelectRow: {
    flexDirection: 'row',
    gap: 8,
  },
  genderOption: {
    flex: 1,
    paddingVertical: 10,
    borderRadius: 8,
    borderWidth: 1,
    borderColor: '#cbd5e1',
    alignItems: 'center',
  },
  femaleActiveOption: {
    backgroundColor: '#ec4899',
    borderColor: '#ec4899',
  },
  maleActiveOption: {
    backgroundColor: '#2563eb',
    borderColor: '#2563eb',
  },
  genderOptionText: {
    color: '#334155',
    fontWeight: '600',
  },
  activeOptionText: {
    color: '#ffffff',
  },
  addButton: {
    backgroundColor: '#16a34a',
    paddingHorizontal: 18,
    justifyContent: 'center',
    borderRadius: 8,
  },
  addButtonText: {
    color: '#ffffff',
    fontWeight: 'bold',
  },
  filterRow: {
    flexDirection: 'row',
    gap: 8,
    marginBottom: 12,
  },
  filterButton: {
    flex: 1,
    paddingVertical: 8,
    borderRadius: 20,
    backgroundColor: '#e2e8f0',
    alignItems: 'center',
  },
  activeFilterButton: {
    backgroundColor: '#0f172a',
  },
  filterText: {
    color: '#334155',
    fontWeight: '600',
    fontSize: 13,
  },
  activeFilterText: {
    color: '#ffffff',
  },
  listGap: {
    gap: 10,
  },
  itemRow: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
    padding: 14,
    borderRadius: 12,
    borderWidth: 2,
  },
  itemName: {
    fontSize: 16,
    fontWeight: 'bold',
    color: '#0f172a',
  },
  itemSub: {
    fontSize: 12,
    color: '#64748b',
    marginTop: 2,
  },
  okeyBtn: {
    paddingVertical: 8,
    paddingHorizontal: 16,
    borderRadius: 8,
  },
  okeyBtnText: {
    color: '#ffffff',
    fontWeight: 'bold',
  },
});
```

---

## 3️⃣ SINAV SENARYOSU 2C — Öğrenci Not Listesi: Yanındaki Butona Basınca Geçti (Yeşil) / Kaldı (Kırmızı) Renk Değişimi

* **İlgili Ders Konusu:** Hafta 6 (`FlatList.md` — `CourseModules`)
* **Bu Kod Ne İşe Yarar?**
  * Hoca sınavda cinsiyet yerine **Not / Başarı Durumu (50 üstü Geçti = Yeşil, 50 altı Kaldı = Kırmızı)** veya **Stok Durumu** sorarsa bu kodu kullanabilirsin.
  * Her öğrencinin yanında **"Sonucu Gör"** butonu vardır; tıklandığında notu `50` ve üzeri olanların kartı yeşil (`#dcfce7`), `50`'nin altında olanların kartı kırmızı (`#fee2e2`) olur.

```jsx
import React, { useState } from 'react';
import { SafeAreaView, FlatList, View, Text, TouchableOpacity, StyleSheet } from 'react-native';

const STUDENTS = [
  { id: '1', name: 'Ayşe Yılmaz', grade: 85 },
  { id: '2', name: 'Ahmet Demir', grade: 42 },
  { id: '3', name: 'Zeynep Kaya', grade: 68 },
  { id: '4', name: 'Mehmet Çelik', grade: 35 },
];

export default function StudentGradeColorList() {
  const [revealed, setRevealed] = useState({});

  const toggleReveal = (id) => {
    setRevealed((prev) => ({ ...prev, [id]: !prev[id] }));
  };

  return (
    <SafeAreaView style={styles.safeArea}>
      <View style={styles.container}>
        <Text style={styles.title}>Öğrenci Sınav Sonuç Listesi</Text>
        <FlatList
          data={STUDENTS}
          keyExtractor={(item) => item.id}
          contentContainerStyle={{ gap: 12 }}
          renderItem={({ item }) => {
            const isShown = !!revealed[item.id];
            const isPassed = item.grade >= 50;

            const cardBg = !isShown ? '#ffffff' : isPassed ? '#dcfce7' : '#fee2e2';
            const borderCol = !isShown ? '#cbd5e1' : isPassed ? '#22c55e' : '#ef4444';
            const btnCol = !isShown ? '#334155' : isPassed ? '#16a34a' : '#dc2626';

            return (
              <View style={[styles.card, { backgroundColor: cardBg, borderColor: borderCol }]}>
                <View>
                  <Text style={styles.studentName}>{item.name}</Text>
                  <Text style={styles.gradeText}>
                    Not: {item.grade} ·{' '}
                    {!isShown ? 'Gizli' : isPassed ? 'GEÇTİ ✓' : 'KALDI ✗'}
                  </Text>
                </View>
                <TouchableOpacity
                  style={[styles.btn, { backgroundColor: btnCol }]}
                  onPress={() => toggleReveal(item.id)}
                >
                  <Text style={styles.btnText}>
                    {isShown ? (isPassed ? 'Geçti' : 'Kaldı') : 'Kontrol Et'}
                  </Text>
                </TouchableOpacity>
              </View>
            );
          }}
        />
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  safeArea: { flex: 1, backgroundColor: '#f8fafc' },
  container: { flex: 1, padding: 20 },
  title: { fontSize: 22, fontWeight: 'bold', color: '#0f172a', marginBottom: 16, textAlign: 'center' },
  card: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
    padding: 16,
    borderRadius: 14,
    borderWidth: 2,
  },
  studentName: { fontSize: 17, fontWeight: 'bold', color: '#0f172a' },
  gradeText: { fontSize: 14, color: '#475569', marginTop: 4 },
  btn: { paddingVertical: 10, paddingHorizontal: 16, borderRadius: 10 },
  btnText: { color: '#ffffff', fontWeight: 'bold' },
});
```

---

## 4️⃣ HAFTA 6 (W6) — Hocanın Orijinal FlatList + Switch ile Renk Değiştiren Kodu (`CourseModules`)

* **Hafta ve Konu Başlığı:** Hafta 6 (W6) · `W6 / components / FlatList.md` · **Example 1: Course Modules with Completion State (`CourseModules`)**
* **Bu Kod Ne İşe Yarar?**
  * `MODULES` dizisindeki dersleri `FlatList` ile alt alta listeler.
  * Her satırın sağında bir `Switch` (aç/kapa anahtarı) vardır.
  * `Switch` açıldığında (`done === true`), kartın arka planı beyazdan açık yeşile (`#dcfce7`), kenarlığı ise yeşile (`#22c55e`) dönüşür.
  * Listenin en altında `ListFooterComponent` ile kaç modülün tamamlandığını (`Completed: X / 4`) gösterir.

```jsx
import React, { useState } from 'react';
import { FlatList, SafeAreaView, Switch, Text, View } from 'react-native';

const MODULES = [
  { id: '1', title: 'Introduction & Setup', duration: 12 },
  { id: '2', title: 'Core Components', duration: 18 },
  { id: '3', title: 'State & Props', duration: 22 },
  { id: '4', title: 'Navigation', duration: 15 },
];

export default function CourseModules() {
  const [completed, setCompleted] = useState({});

  const toggleModule = (id, value) => {
    setCompleted((prev) => ({ ...prev, [id]: value }));
  };

  return (
    <SafeAreaView style={{ flex: 1, backgroundColor: '#f8fafc' }}>
      <View style={{ padding: 24, gap: 16, flex: 1 }}>
        <Text style={{ fontSize: 22, fontWeight: '700', color: '#0f172a' }}>
          Course Modules
        </Text>
        <FlatList
          data={MODULES}
          keyExtractor={(item) => item.id}
          ItemSeparatorComponent={() => <View style={{ height: 12 }} />}
          contentContainerStyle={{ paddingBottom: 24 }}
          renderItem={({ item }) => {
            const done = completed[item.id];
            return (
              <View
                style={{
                  padding: 18,
                  borderRadius: 16,
                  borderWidth: 1,
                  borderColor: done ? '#22c55e' : '#e2e8f0',
                  backgroundColor: done ? '#dcfce7' : '#fff',
                  flexDirection: 'row',
                  alignItems: 'center',
                  justifyContent: 'space-between',
                }}
              >
                <View style={{ gap: 4 }}>
                  <Text style={{ fontSize: 16, fontWeight: '600' }}>
                    {item.title}
                  </Text>
                  <Text style={{ color: '#475569' }}>
                    Duration: {item.duration} min
                  </Text>
                </View>
                <Switch
                  value={done}
                  onValueChange={(value) => toggleModule(item.id, value)}
                />
              </View>
            );
          }}
          ListFooterComponent={() => {
            const total = MODULES.length;
            const doneCount = Object.values(completed).filter(Boolean).length;
            return (
              <Text style={{ marginTop: 16, textAlign: 'center', color: '#1f2937' }}>
                Completed: {doneCount} / {total}
              </Text>
            );
          }}
        />
      </View>
    </SafeAreaView>
  );
}
```

---

## 5️⃣ HAFTA 6 (W6) — Hocanın Orijinal Checkbox Görev Listesi Kodu (`LessonChecklist`)

* **Hafta ve Konu Başlığı:** Hafta 6 (W6) · `W6 / components / Checkbox.md` · **Example 1: Lesson Task List (`LessonChecklist`)**
* **Bu Kod Ne İşe Yarar?**
  * `expo-checkbox` paketini kullanarak görevlerin soluna onay kutusu koyar (Snack Expo'da `expo-checkbox` import edildiğinde sağ altta çıkan **Add dependency** butonuna basarak paketi ekleyebilirsin).
  * Kutu işaretlendiğinde (`completed[task.id] === true`), kutu rengi yeşil (`#22c55e`) olur ve yanındaki görev metninin üstü çizilir (`textDecorationLine: 'line-through'`).

```jsx
import React, { useState } from 'react';
import { SafeAreaView, View, Text } from 'react-native';
import Checkbox from 'expo-checkbox';

const TASKS = [
  { id: 'slides', label: 'Review the new slides' },
  { id: 'demo', label: 'Run the Image + ScrollView demo' },
  { id: 'prep', label: 'Draft the Q&A scenarios' },
];

export default function LessonChecklist() {
  const [completed, setCompleted] = useState({});

  const toggleTask = (taskId, value) => {
    setCompleted((prev) => ({ ...prev, [taskId]: value }));
  };

  return (
    <SafeAreaView style={{ flex: 1, backgroundColor: '#0f172a', padding: 24, gap: 16 }}>
      <Text style={{ color: '#e2e8f0', fontSize: 22, fontWeight: '700' }}>W6 Prep</Text>
      {TASKS.map((task) => (
        <View
          key={task.id}
          style={{ flexDirection: 'row', alignItems: 'center', gap: 12, paddingVertical: 8 }}
        >
          <Checkbox
            value={!!completed[task.id]}
            onValueChange={(value) => toggleTask(task.id, value)}
            color={completed[task.id] ? '#22c55e' : undefined}
            style={{ width: 22, height: 22, borderRadius: 6 }}
          />
          <Text
            style={{
              color: '#e2e8f0',
              textDecorationLine: completed[task.id] ? 'line-through' : 'none',
            }}
          >
            {task.label}
          </Text>
        </View>
      ))}
    </SafeAreaView>
  );
}
```

---

## 6️⃣ HAFTA 6 (W6) — Hocanın Orijinal Katılımcı Ayarları Checkbox + Aktifleşen Kaydet Butonu Kodu (`ParticipantSettings`)

* **Hafta ve Konu Başlığı:** Hafta 6 (W6) · `W6 / components / Checkbox.md` · **Example 2: Participant Settings Form (`ParticipantSettings`)**
* **Bu Kod Ne İşe Yarar?**
  * Her satırda yazı solda, `Checkbox` sağda (`justifyContent: 'space-between'`) yer alır.
  * `Object.values(options).some(Boolean)` ile en az bir kutunun seçili olup olmadığını kontrol eder (`allActive`).
  * Hiçbir kutu seçili değilken alttaki **Save Settings** butonu gri (`#334155`) ve tıklanamaz (`disabled={!allActive}`) durumdadır; en az bir kutu seçildiğinde buton açık mavi (`#38bdf8`) ve tıklanabilir hale gelir!

```jsx
import React, { useMemo, useState } from 'react';
import { SafeAreaView, View, Text, TouchableOpacity } from 'react-native';
import Checkbox from 'expo-checkbox';

const SETTINGS = [
  { id: 'recordings', label: 'Share session recordings' },
  { id: 'reminders', label: 'Send a reminder 1 hour before class' },
  { id: 'survey', label: 'Trigger a mini survey after each lesson' },
];

export default function ParticipantSettings() {
  const [options, setOptions] = useState(
    SETTINGS.reduce((acc, item) => ({ ...acc, [item.id]: false }), {})
  );

  const allActive = useMemo(() => Object.values(options).some(Boolean), [options]);

  const toggle = (key, value) => {
    setOptions((prev) => ({ ...prev, [key]: value }));
  };

  return (
    <SafeAreaView style={{ flex: 1, backgroundColor: '#020617', padding: 24 }}>
      <Text style={{ color: '#e2e8f0', fontSize: 20, fontWeight: '600', marginBottom: 16 }}>
        Participant Settings
      </Text>
      {SETTINGS.map((setting) => (
        <View
          key={setting.id}
          style={{
            flexDirection: 'row',
            alignItems: 'center',
            justifyContent: 'space-between',
            paddingVertical: 12,
          }}
        >
          <Text style={{ color: '#e2e8f0', fontSize: 16 }}>{setting.label}</Text>
          <Checkbox
            value={options[setting.id]}
            onValueChange={(value) => toggle(setting.id, value)}
            color={options[setting.id] ? '#38bdf8' : undefined}
          />
        </View>
      ))}

      <TouchableOpacity
        style={{
          marginTop: 32,
          backgroundColor: allActive ? '#38bdf8' : '#334155',
          borderRadius: 16,
          paddingVertical: 16,
          alignItems: 'center',
        }}
        disabled={!allActive}
      >
        <Text style={{ color: '#0f172a', fontWeight: '700' }}>Save Settings</Text>
      </TouchableOpacity>
    </SafeAreaView>
  );
}
```
