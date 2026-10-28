# 🧮 Hesap Makinesi (Toplama ve 4 İşlem), Form Doğrulama, Karakter Sayacı ve Canlı Arama Senaryoları

> **[⬅️ Ana Sınav Rehberine (README) Dön](./README.md)**

![Hesap Makinesi, Form ve Arama Görsel Rehberi](./gorseller/05-hesap-makinesi-form-arama.svg)

---

## 📌 Bu Dosya Hangi Hafta ve Hangi Ders Kodlarına Karşılık Gelir?

| Hafta | Ders Notu Dosyası ve Konu Başlığı | Hocanın Kodundaki Bileşen Adı | Ne İşe Yarar? |
| :--- | :--- | :--- | :--- |
| **Hafta 6 (W6)** | `W6 / components / Button.md` — **Example 1: Sum Calculator** | `SumCalculator` | İki adet sayısal `TextInput` (`First number`, `Second number`) ve `Calculate sum` butonu ile iki sayıyı toplar, sonucu mavi büyük yazıyla gösterir. |
| **Hafta 4 (W4)** | `W4 / 5-react-native-state.md` — **Example 2: Form State Management** | `SimpleForm` | İsim ve E-posta inputları alır; boşsa hata uyarısı (`Alert.alert`) verir, doluysa yeşil başarı kutusu (`#d4edda`) ve `New Form` sıfırlama butonu gösterir. |
| **Hafta 4 (W4)** | `W4 / 6-react-native-hooks.md` — **Example 2: Text Input** | `TextInputExample` | Kullanıcının yazdığı metni (`You wrote: {text}`) ve karakter sayısını (`Character count: {text.length}`) anlık olarak ekranda gösterir. |
| **Hafta 6 (W6)** | `W6 / components / Text.md` — **Example 2: Dynamic Label with Character Counter** | `BioField` | `120` karakter sınırlı çok satırlı (`multiline`) inputta kalan karakter sayısını (`120 - bio.length`) hesaplar; `10` ve altına inince rengi turuncu (`#f97316`) yapar. |
| **Hafta 6 (W6)** | `W6 / components / TextInput.md` — **Example 1: Email Field with Instant Validation** | `EmailField` | E-posta adresini `EMAIL_REGEX` ile kontrol eder; doğruysa çerçeveyi ve mesajı yeşil (`#22c55e`), yanlışsa kırmızı (`#ef4444`) yapar. |
| **Hafta 6 (W6)** | `W6 / components / TextInput.md` — **Example 2: Search Bar Filtering a List** | `SearchableList` | Arama kutusuna yazılan kelimeye göre `LESSONS` dizisini `.filter()` ve `.includes()` ile süzer; eşleşme yoksa bilgi kutusu gösterir. |

---

## ⚡ Sınavda Hoca Input, Hesap Makinesi veya Form Üzerinde Değişiklik İsterse Nereyi Değiştireceksin?

| Hocanın Görselde İstediği Değişiklik | Kodda Değiştireceğin Satır |
| :--- | :--- |
| Toplama yerine **Çarpma / Çıkarma / Bölme** yapmak | `const total = Number(first) + Number(second);` satırındaki `+` yerine `*`, `-` veya `/` yaz |
| Inputu **Şifre Alanına** (yıldızlı/gizli) çevirmek | `<TextInput secureTextEntry={true} ... />` ekle |
| Inputta **Sadece Rakam Klavyesi** açtırmak | `keyboardType="numeric"` |
| Inputa **Maksimum Karakter Sınırı** koymak | `maxLength={120}` |
| Inputu **Çok Satırlı (Büyük Metin Kutusu)** yapmak | `multiline={true}` ve stilinde `minHeight: 120, textAlignVertical: 'top'` |
| Formda **Yeni Bir Alan (Örn. Telefon veya Yaş)** eklemek | `const [phone, setPhone] = useState('');` tanımla ve bir `<TextInput value={phone} onChangeText={setPhone} />` daha ekle |

---

## 1️⃣ HAFTA 6 (W6) — Hocanın Orijinal İki Sayıyı Toplama Kodu (`SumCalculator`)

* **Hafta ve Konu Başlığı:** Hafta 6 (W6) · `W6 / components / Button.md` · **Example 1: Sum Calculator (`SumCalculator`)**
* **Bu Kod Ne İşe Yarar?**
  * `first` ve `second` state'lerinde iki metin kutusunun değerini tutar.
  * `Calculate sum` butonuna basılınca `Number(first) + Number(second)` ile toplamı hesaplar ve `result` state'ine yazar.
  * Henüz hesaplama yapılmadıysa (`result === null`) `'Enter two valid numbers'`, yapıldıysa toplam sonucu mavi (`#2563eb`) ve kalın (`fontSize: 24`) olarak ekrana yazar.

```jsx
import React, { useState } from 'react';
import { Button, SafeAreaView, Text, TextInput, View } from 'react-native';

export default function SumCalculator() {
  const [first, setFirst] = useState('');
  const [second, setSecond] = useState('');
  const [result, setResult] = useState(null);

  const handleSum = () => {
    const total = Number(first) + Number(second);
    setResult(Number.isFinite(total) ? total : null);
  };

  return (
    <SafeAreaView style={{ flex: 1, backgroundColor: '#f8fafc' }}>
      <View
        style={{
          flex: 1,
          justifyContent: 'center',
          padding: 24,
          gap: 16,
        }}
      >
        <Text style={{ fontSize: 20, fontWeight: '600', color: '#0f172a' }}>
          Add two numbers
        </Text>
        <View
          style={{
            borderRadius: 16,
            backgroundColor: '#fff',
            padding: 20,
            gap: 16,
            shadowColor: '#000',
            shadowOpacity: 0.05,
            shadowRadius: 12,
            elevation: 2,
          }}
        >
          <TextInput
            placeholder="First number"
            keyboardType="numeric"
            value={first}
            onChangeText={setFirst}
            style={{
              borderWidth: 1,
              borderColor: '#d4d4d8',
              borderRadius: 10,
              paddingHorizontal: 12,
              paddingVertical: 12,
            }}
          />
          <TextInput
            placeholder="Second number"
            keyboardType="numeric"
            value={second}
            onChangeText={setSecond}
            style={{
              borderWidth: 1,
              borderColor: '#d4d4d8',
              borderRadius: 10,
              paddingHorizontal: 12,
              paddingVertical: 12,
            }}
          />
          <Button title="Calculate sum" onPress={handleSum} />
          <View>
            <Text style={{ color: '#475569' }}>Result:</Text>
            <Text style={{ fontSize: 24, fontWeight: '700', color: '#2563eb' }}>
              {result === null ? 'Enter two valid numbers' : result}
            </Text>
          </View>
        </View>
      </View>
    </SafeAreaView>
  );
}
```

---

## 2️⃣ SINAV SENARYOSU 5A — 4 İşlem Hesap Makinesi (Toplama, Çıkarma, Çarpma, Bölme + Temizle Butonu)

* **İlgili Ders Konusu:** Hafta 6 (`W6 / Button.md` — `SumCalculator` genişletilmiş sınav versiyonu)
* **Bu Kod Ne İşe Yarar?**
  * Hocanın `SumCalculator` koduna yan yana **Topla (`+`), Çıkar (`-`), Çarp (`×`), Böl (`÷`)** butonları ve **Temizle (`Reset`)** butonu eklenmiş halidir.
  * Hangi işleme basıldıysa onu yapar ve seçili işlem butonunun rengini vurgular.

```jsx
import React, { useState } from 'react';
import { SafeAreaView, View, Text, TextInput, TouchableOpacity, StyleSheet } from 'react-native';

export default function FourOperationsCalculator() {
  const [first, setFirst] = useState('');
  const [second, setSecond] = useState('');
  const [result, setResult] = useState(null);
  const [operationName, setOperationName] = useState('');

  const calculate = (op) => {
    const n1 = Number(first);
    const n2 = Number(second);
    if (first.trim() === '' || second.trim() === '' || !Number.isFinite(n1) || !Number.isFinite(n2)) {
      setResult('Lütfen iki geçerli sayı girin');
      return;
    }
    if (op === '+') {
      setResult(n1 + n2);
      setOperationName('Toplama Sonucu');
    } else if (op === '-') {
      setResult(n1 - n2);
      setOperationName('Çıkarma Sonucu');
    } else if (op === '*') {
      setResult(n1 * n2);
      setOperationName('Çarpma Sonucu');
    } else if (op === '/') {
      setResult(n2 !== 0 ? (n1 / n2).toFixed(2) : 'Sıfıra bölünemez!');
      setOperationName('Bölme Sonucu');
    }
  };

  const handleReset = () => {
    setFirst('');
    setSecond('');
    setResult(null);
    setOperationName('');
  };

  return (
    <SafeAreaView style={styles.safeArea}>
      <View style={styles.container}>
        <Text style={styles.title}>Dört İşlem Hesap Makinesi</Text>

        <View style={styles.card}>
          <TextInput
            placeholder="Birinci sayıyı girin"
            keyboardType="numeric"
            value={first}
            onChangeText={setFirst}
            style={styles.input}
          />
          <TextInput
            placeholder="İkinci sayıyı girin"
            keyboardType="numeric"
            value={second}
            onChangeText={setSecond}
            style={styles.input}
          />

          <View style={styles.opRow}>
            <TouchableOpacity style={[styles.opBtn, { backgroundColor: '#16a34a' }]} onPress={() => calculate('+')}>
              <Text style={styles.opText}>+ Topla</Text>
            </TouchableOpacity>
            <TouchableOpacity style={[styles.opBtn, { backgroundColor: '#ea580c' }]} onPress={() => calculate('-')}>
              <Text style={styles.opText}>- Çıkar</Text>
            </TouchableOpacity>
            <TouchableOpacity style={[styles.opBtn, { backgroundColor: '#9333ea' }]} onPress={() => calculate('*')}>
              <Text style={styles.opText}>× Çarp</Text>
            </TouchableOpacity>
            <TouchableOpacity style={[styles.opBtn, { backgroundColor: '#2563eb' }]} onPress={() => calculate('/')}>
              <Text style={styles.opText}>÷ Böl</Text>
            </TouchableOpacity>
          </View>

          <TouchableOpacity style={styles.resetBtn} onPress={handleReset}>
            <Text style={styles.resetText}>Temizle (Reset)</Text>
          </TouchableOpacity>

          <View style={styles.resultBox}>
            <Text style={styles.resultLabel}>{operationName || 'Sonuç:'}</Text>
            <Text style={styles.resultValue}>
              {result === null ? 'Henüz işlem seçilmedi' : result}
            </Text>
          </View>
        </View>
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  safeArea: { flex: 1, backgroundColor: '#f8fafc' },
  container: { flex: 1, justifyContent: 'center', padding: 24 },
  title: { fontSize: 22, fontWeight: 'bold', color: '#0f172a', marginBottom: 16, textAlign: 'center' },
  card: {
    backgroundColor: '#ffffff',
    borderRadius: 16,
    padding: 20,
    gap: 14,
    borderWidth: 1,
    borderColor: '#e2e8f0',
  },
  input: {
    borderWidth: 1,
    borderColor: '#cbd5e1',
    borderRadius: 10,
    paddingHorizontal: 14,
    paddingVertical: 12,
    fontSize: 16,
  },
  opRow: { flexDirection: 'row', justifyContent: 'space-between', gap: 8 },
  opBtn: { flex: 1, paddingVertical: 12, borderRadius: 10, alignItems: 'center' },
  opText: { color: '#ffffff', fontWeight: 'bold', fontSize: 14 },
  resetBtn: { backgroundColor: '#dc2626', paddingVertical: 12, borderRadius: 10, alignItems: 'center' },
  resetText: { color: '#ffffff', fontWeight: 'bold', fontSize: 15 },
  resultBox: { backgroundColor: '#f1f5f9', padding: 14, borderRadius: 12, alignItems: 'center' },
  resultLabel: { fontSize: 14, color: '#475569', marginBottom: 4 },
  resultValue: { fontSize: 24, fontWeight: 'bold', color: '#2563eb' },
});
```

---

## 3️⃣ HAFTA 4 (W4) — Hocanın Orijinal Form ve Başarı Kutusu Kodu (`SimpleForm`)

* **Hafta ve Konu Başlığı:** Hafta 4 (W4) · `W4 / 5-react-native-state.md` · **Example 2: Form State Management (`SimpleForm`)**
* **Bu Kod Ne İşe Yarar?**
  * Kullanıcının adını (`name`) ve e-postasını (`email`) alır.
  * Yeşil **Submit** (`#28A745`) butonuna basıldığında alanlardan biri boşsa `Alert.alert('Error', 'Please fill all fields')` uyarısı verir.
  * İkisi de doluysa `isSubmitted` state'ini `true` yapar ve altta yeşil arka planlı (`#d4edda`) başarı kutusunu (`Form submitted successfully!`) ve formu temizleyen **New Form** butonunu gösterir.

```jsx
import React, { useState } from 'react';
import { View, Text, TextInput, TouchableOpacity, StyleSheet, Alert } from 'react-native';

export default function SimpleForm() {
  const [name, setName] = useState('');
  const [email, setEmail] = useState('');
  const [isSubmitted, setIsSubmitted] = useState(false);

  const handleSubmit = () => {
    if (name.trim() === '' || email.trim() === '') {
      Alert.alert('Error', 'Please fill all fields');
      return;
    }
    
    setIsSubmitted(true);
    Alert.alert('Success', `Hello ${name}! Email: ${email}`);
  };

  const resetForm = () => {
    setName('');
    setEmail('');
    setIsSubmitted(false);
  };

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Simple Form</Text>
      
      <TextInput
        style={styles.input}
        placeholder="Enter your name"
        value={name}
        onChangeText={setName}
      />
      
      <TextInput
        style={styles.input}
        placeholder="Enter your email"
        value={email}
        onChangeText={setEmail}
        keyboardType="email-address"
      />
      
      <TouchableOpacity style={styles.submitButton} onPress={handleSubmit}>
        <Text style={styles.buttonText}>Submit</Text>
      </TouchableOpacity>
      
      {isSubmitted && (
        <View style={styles.successContainer}>
          <Text style={styles.successText}>Form submitted successfully!</Text>
          <TouchableOpacity style={styles.resetButton} onPress={resetForm}>
            <Text style={styles.buttonText}>New Form</Text>
          </TouchableOpacity>
        </View>
      )}
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    justifyContent: 'center',
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    textAlign: 'center',
    marginBottom: 30,
    color: '#333',
  },
  input: {
    borderWidth: 1,
    borderColor: '#ccc',
    borderRadius: 8,
    padding: 12,
    fontSize: 16,
    marginBottom: 15,
    backgroundColor: 'white',
  },
  submitButton: {
    backgroundColor: '#28A745',
    padding: 15,
    borderRadius: 8,
    alignItems: 'center',
    marginBottom: 20,
  },
  resetButton: {
    backgroundColor: '#6C757D',
    padding: 10,
    borderRadius: 8,
    alignItems: 'center',
    marginTop: 10,
  },
  buttonText: {
    color: 'white',
    fontSize: 16,
    fontWeight: '600',
  },
  successContainer: {
    backgroundColor: '#d4edda',
    padding: 15,
    borderRadius: 8,
    borderWidth: 1,
    borderColor: '#c3e6cb',
  },
  successText: {
    color: '#155724',
    fontSize: 16,
    textAlign: 'center',
    marginBottom: 10,
  },
});
```

---

## 4️⃣ HAFTA 4 (W4) & HAFTA 6 (W6) — Hocanın Orijinal Karakter Sayacı Kodları (`TextInputExample` ve `BioField`)

### A) Hafta 4 — `TextInputExample` (`W4 / 6-react-native-hooks.md` — Example 2)
* **Bu Kod Ne İşe Yarar?**
  * Kullanıcının yazdığı metni anında altında (`You wrote: {text}`) ve harf sayısını (`Character count: {text.length}`) gösterir.

```jsx
import React, { useState } from 'react';
import { View, Text, TextInput, StyleSheet } from 'react-native';

export default function TextInputExample() {
  const [text, setText] = useState('');

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Text Input</Text>
      
      <TextInput
        style={styles.input}
        placeholder="Write something..."
        value={text}
        onChangeText={setText}
      />
      
      <Text style={styles.displayText}>
        You wrote: {text}
      </Text>
      
      <Text style={styles.countText}>
        Character count: {text.length}
      </Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    justifyContent: 'center',
  },
  title: {
    fontSize: 20,
    fontWeight: 'bold',
    marginBottom: 20,
    textAlign: 'center',
  },
  input: {
    borderWidth: 1,
    borderColor: '#ccc',
    borderRadius: 8,
    padding: 12,
    fontSize: 16,
    marginBottom: 20,
  },
  displayText: {
    fontSize: 16,
    marginBottom: 10,
    color: '#333',
  },
  countText: {
    fontSize: 14,
    color: '#666',
  },
});
```

### B) Hafta 6 — `BioField` (`W6 / components / Text.md` — Example 2)
* **Bu Kod Ne İşe Yarar?**
  * `MAX_LENGTH = 120` karakter sınırı olan çok satırlı (`multiline`) bir biyografi kutusudur.
  * Kalan karakter sayısı `10` veya daha az olduğunda (`limitReached = remaining <= 10`), altındaki sayaç yazısı gri (`#475569`) renkten turuncuya (`#f97316`) döner.

```jsx
import React, { useState } from 'react';
import { SafeAreaView, Text, TextInput, View } from 'react-native';

const MAX_LENGTH = 120;

export default function BioField() {
  const [bio, setBio] = useState('');
  const remaining = MAX_LENGTH - bio.length;
  const limitReached = remaining <= 10;

  return (
    <SafeAreaView style={{ flex: 1, backgroundColor: '#f8fafc' }}>
      <View
        style={{
          flex: 1,
          justifyContent: 'center',
          padding: 24,
          gap: 12,
        }}
      >
        <Text style={{ fontSize: 22, fontWeight: '700', color: '#0f172a' }}>
          Profile Summary
        </Text>
        <View
          style={{
            borderRadius: 16,
            backgroundColor: '#fff',
            padding: 20,
            gap: 12,
            shadowColor: '#000',
            shadowOpacity: 0.05,
            shadowRadius: 10,
            elevation: 2,
          }}
        >
          <TextInput
            multiline
            maxLength={MAX_LENGTH}
            value={bio}
            onChangeText={setBio}
            placeholder="Introduce yourself in a few sentences..."
            style={{
              minHeight: 120,
              borderWidth: 1,
              borderColor: '#d4d4d8',
              borderRadius: 10,
              padding: 14,
              textAlignVertical: 'top',
            }}
          />
          <Text style={{ color: limitReached ? '#f97316' : '#475569' }}>
            Characters remaining: {remaining}
          </Text>
        </View>
      </View>
    </SafeAreaView>
  );
}
```

---

## 5️⃣ HAFTA 6 (W6) — Hocanın Orijinal Canlı E-Posta Doğrulama Kodu (`EmailField`)

* **Hafta ve Konu Başlığı:** Hafta 6 (W6) · `W6 / components / TextInput.md` · **Example 1: Email Field with Instant Validation (`EmailField`)**
* **Bu Kod Ne İşe Yarar?**
  * Kullanıcı e-posta yazarken `EMAIL_REGEX.test(value)` ile formatın geçerli olup olmadığını anında kontrol eder.
  * Kutu boşsa çerçeve gri (`#334155`), geçerliyse yeşil (`#22c55e`), geçersizse kırmızı (`#ef4444`) olur ve altındaki durum yazısı renk değiştirir.

```jsx
import React, { useState } from 'react';
import { SafeAreaView, Text, TextInput, View } from 'react-native';

const EMAIL_REGEX = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;

export default function EmailField() {
  const [value, setValue] = useState('');
  const isValid = EMAIL_REGEX.test(value);

  return (
    <SafeAreaView style={{ flex: 1, backgroundColor: '#0f172a' }}>
      <View
        style={{
          flex: 1,
          justifyContent: 'center',
          padding: 24,
        }}
      >
        <View
          style={{
            borderRadius: 16,
            backgroundColor: '#1f2937',
            padding: 24,
            gap: 16,
          }}
        >
          <Text style={{ fontSize: 20, fontWeight: '600', color: '#f1f5f9' }}>
            Verify your email address
          </Text>
          <TextInput
            value={value}
            onChangeText={setValue}
            keyboardType="email-address"
            autoCapitalize="none"
            placeholder="name@example.com"
            placeholderTextColor="#94a3b8"
            style={{
              borderWidth: 1,
              borderColor:
                value.length === 0
                  ? '#334155'
                  : isValid
                  ? '#22c55e'
                  : '#ef4444',
              borderRadius: 10,
              paddingHorizontal: 14,
              paddingVertical: 12,
              color: '#f8fafc',
            }}
          />
          <Text style={{ color: isValid ? '#22c55e' : '#f97316' }}>
            {value.length === 0
              ? 'Start typing your email address.'
              : isValid
              ? 'Looks like a valid address.'
              : 'Please enter a valid email address.'}
          </Text>
        </View>
      </View>
    </SafeAreaView>
  );
}
```

---

## 6️⃣ HAFTA 6 (W6) — Hocanın Orijinal Canlı Arama Çubuğu ve Liste Filtreleme Kodu (`SearchableList`)

* **Hafta ve Konu Başlığı:** Hafta 6 (W6) · `W6 / components / TextInput.md` · **Example 2: Search Bar Filtering a List (`SearchableList`)**
* **Bu Kod Ne İşe Yarar?**
  * Arama kutusuna (`TextInput`) yazılan kelimeyi küçük harfe çevirip (`query.toLowerCase()`), `LESSONS` listesindeki başlıkların içinde arar (`lesson.title.toLowerCase().includes(lowered)`).
  * Eşleşen dersleri mavi kartlar (`#e0f2fe`) halinde listeler; hiçbir ders eşleşmezse `ListEmptyComponent` devreye girer ve `"No lessons match your search."` yazar.

```jsx
import React, { useMemo, useState } from 'react';
import { FlatList, SafeAreaView, Text, TextInput, View } from 'react-native';

const LESSONS = [
  { id: '1', title: 'Intro to React Native' },
  { id: '2', title: 'Working with Expo' },
  { id: '3', title: 'Navigation Basics' },
  { id: '4', title: 'State Management' },
  { id: '5', title: 'Performance Tips' },
];

export default function SearchableList() {
  const [query, setQuery] = useState('');

  const filteredLessons = useMemo(() => {
    const lowered = query.toLowerCase();
    return LESSONS.filter((lesson) =>
      lesson.title.toLowerCase().includes(lowered)
    );
  }, [query]);

  return (
    <SafeAreaView style={{ flex: 1, backgroundColor: '#f8fafc' }}>
      <View style={{ flex: 1, padding: 24, gap: 16 }}>
        <Text style={{ fontSize: 22, fontWeight: '700', color: '#0f172a' }}>
          Search the lesson archive
        </Text>
        <TextInput
          value={query}
          onChangeText={setQuery}
          placeholder="Search lessons..."
          returnKeyType="search"
          style={{
            borderWidth: 1,
            borderColor: '#cbd5f5',
            borderRadius: 12,
            paddingHorizontal: 16,
            paddingVertical: 14,
            backgroundColor: '#fff',
          }}
        />
        <FlatList
          data={filteredLessons}
          keyExtractor={(item) => item.id}
          ListEmptyComponent={
            <View
              style={{
                padding: 16,
                borderRadius: 12,
                backgroundColor: '#e0f2fe',
              }}
            >
              <Text style={{ color: '#1f2937' }}>
                No lessons match your search.
              </Text>
            </View>
          }
          renderItem={({ item }) => (
            <View
              style={{
                padding: 16,
                borderRadius: 12,
                backgroundColor: '#e0f2fe',
              }}
            >
              <Text style={{ fontWeight: '600', color: '#0f172a' }}>
                {item.title}
              </Text>
            </View>
          )}
          ItemSeparatorComponent={() => <View style={{ height: 12 }} />}
          contentContainerStyle={{ paddingBottom: 24 }}
        />
      </View>
    </SafeAreaView>
  );
}
```
