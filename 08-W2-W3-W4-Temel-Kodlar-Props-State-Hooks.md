# ⚛️ Hafta 2 (W2), Hafta 3 (W3) ve Hafta 4 (W4) Tüm Temel Kodlar (JS ES6, Props, State, Koşullu Render, Hooks)

> **[⬅️ Ana Sınav Rehberine (README) Dön](./README.md)**

---

## 📌 Bu Dosya Hangi Hafta ve Hangi Ders Kodlarına Karşılık Gelir?

| Hafta | Ders Notu Dosyası ve Konu Başlığı | Hocanın Kodundaki Bileşen / Fonksiyon Adı | Ne İşe Yarar? |
| :--- | :--- | :--- | :--- |
| **Hafta 2 (W2)** | `W2 / topics / 06_control_flow.js` | `getSuggestedActivity` (Hava Durumu Önerisi) | Seçilen hava durumuna (`sunny`, `rainy`, `windy`, `snowy`) göre `if/else` ile kıyafet, `switch/case` ile aktivite önerir. |
| **Hafta 2 (W2)** | `W2 / topics / 08_functions.js` | `calculateTax` (Gelir ve Vergi Hesaplama) | Gelir (`income`) ve vergi oranını (`rate`) alıp vergiyi hesaplar ve para birimi formatında gösterir. |
| **Hafta 2 (W2)** | `W2 / topics / 09_arrays.js` | `songs.map / filter / reduce` (Çalma Listesi Özeti) | Şarkı listesindeki toplam süreyi `.reduce()` ile toplar, 5 dakikadan uzun şarkıları `.filter()` ile bulur. |
| **Hafta 3 (W3)** | `W3 / 07-conditional-rendering-example.jsx` | `BasicConditional`, `MultipleConditions`, `ConditionalList` | Giriş/Çıkış (`isLoggedIn`), Kullanıcı Tipi (`guest`, `user`, `admin` + `isVerified`) ve Ürün Stok/Kategori filtreleme (`inStock`, `fruit`, `vegetable`) yapar. |
| **Hafta 3 (W3)** | `W3 / 10-data-sharing-example.jsx` | `TodoApp` (`useReducer`), `ThemeProvider` (`Context`) | `useReducer` ile görev ekleme, üstünü çizme, silme ve `all / active / completed` filtreleme yapar. |
| **Hafta 4 (W4)** | `W4 / 2-example-hello-expo.md` | `App` (Basic Hello React Native) | `Hello React Native 🚀` başlığını ve `Platform.OS` / `Platform.Version` bilgisini gösterir. |
| **Hafta 4 (W4)** | `W4 / 4-react-native-props.md` | `Greeting`, `ParentComponent` & `ChildComponent` | Varsayılan (`default`) prop kullanımını ve alt bileşenden üst bileşene fonksiyon prop ile veri göndermeyi gösterir. |
| **Hafta 4 (W4)** | `W4 / 6-react-native-hooks.md` | `Counter`, `WelcomeMessage` | `useEffect` ve `setTimeout` ile uygulama açıldıktan 2 saniye sonra `'Loading...'` yazısını `'Welcome!'` yapar. |
| **Hafta 4 (W4)** | `W4 / 7-example-basic-components.md` | `ScrollViewExamples`, `TouchableOpacityExamples`, `TextInputExamples` | 20 elemanlı kaydırma listesi, sayaçlı buton ve anlık isim/e-posta yazdırma örneklerini gösterir. |

---

## 1️⃣ HAFTA 4 (W4) — Hocanın Orijinal İlk Expo Ekranı Kodu (`Hello React Native 🚀`)

* **Hafta ve Konu Başlığı:** Hafta 4 (W4) · `W4 / 2-example-hello-expo.md` · **Basic App.js**
* **Bu Kod Ne İşe Yarar?**
  * Ekranın tam ortasında `Hello React Native 🚀` başlığını, altında cihazın işletim sistemini (`Platform.OS` ve `Platform.Version`) ve açıklama metnini gösterir.

```jsx
import React from 'react';
import { StatusBar } from 'expo-status-bar';
import { StyleSheet, Text, View, SafeAreaView, Platform } from 'react-native';

export default function App() {
  return (
    <SafeAreaView style={styles.container}>
      <View style={styles.content}>
        <Text style={styles.title}>Hello React Native 🚀</Text>
        <Text style={styles.subtitle}>
          Platform: {Platform.OS} {Platform.Version}
        </Text>
        <Text style={styles.description}>
          This app is created with Expo and works cross-platform.
        </Text>
      </View>
      <StatusBar style="auto" />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f7fafc',
  },
  content: {
    flex: 1,
    alignItems: 'center',
    justifyContent: 'center',
    paddingHorizontal: 20,
  },
  title: {
    fontSize: 28,
    fontWeight: 'bold',
    color: '#2d3748',
    marginBottom: 16,
    textAlign: 'center',
  },
  subtitle: {
    fontSize: 16,
    color: '#4a5568',
    marginBottom: 12,
    fontWeight: '500',
  },
  description: {
    fontSize: 14,
    color: '#718096',
    textAlign: 'center',
    lineHeight: 20,
  },
});
```

---

## 2️⃣ HAFTA 4 (W4) — Hocanın 2 Saniye Sonra Değişen Karşılama Mesajı Kodu (`WelcomeMessage`)

* **Hafta ve Konu Başlığı:** Hafta 4 (W4) · `W4 / 6-react-native-hooks.md` · **useEffect Example 1: Message on Page Load (`WelcomeMessage`)**
* **Bu Kod Ne İşe Yarar?**
  * Ekran ilk açıldığında `'Loading...'` yazar.
  * `useEffect` içindeki `setTimeout` sayesinde 2000 milisaniye (2 saniye) sonra `message` state'ini `'Welcome!'` olarak günceller.

```jsx
import React, { useState, useEffect } from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function WelcomeMessage() {
  const [message, setMessage] = useState('Loading...');

  useEffect(() => {
    const timer = setTimeout(() => {
      setMessage('Welcome!');
    }, 2000);
    return () => clearTimeout(timer);
  }, []);

  return (
    <View style={styles.container}>
      <Text style={styles.message}>{message}</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  message: {
    fontSize: 20,
    fontWeight: 'bold',
    color: '#007AFF',
  },
});
```

---

## 3️⃣ HAFTA 4 (W4) — Hocanın Varsayılan Props ve Alt Bileşenden Üst Bileşene Veri Gönderme Kodu

* **Hafta ve Konu Başlığı:** Hafta 4 (W4) · `W4 / 4-react-native-props.md` · **Default Props (`Greeting`) & Sending Functions as Props (`ParentComponent`)**
* **Bu Kod Ne İşe Yarar?**
  * `Greeting` bileşenine `name` veya `age` prop'u gönderilmezse varsayılan olarak `name = 'Guest'` ve `age = 0` değerlerini kullanır.
  * `ChildComponent` içindeki butona basıldığında üst bileşendeki `handleChildClick('Hello!')` fonksiyonunu çalıştırır.

```jsx
import React, { useState } from 'react';
import { SafeAreaView, View, Text, TouchableOpacity, StyleSheet, Alert } from 'react-native';

function Greeting({ name = 'Guest', age = 0 }) {
  return (
    <View style={styles.card}>
      <Text style={styles.greetingText}>
        Hello {name}! Your age: {age}
      </Text>
    </View>
  );
}

function ChildComponent({ onButtonClick }) {
  return (
    <TouchableOpacity
      style={styles.button}
      onPress={() => onButtonClick('Hello from Child Component!')}
    >
      <Text style={styles.buttonText}>Send Message to Parent</Text>
    </TouchableOpacity>
  );
}

export default function PropsAdvancedExamples() {
  const [receivedMessage, setReceivedMessage] = useState('Henüz mesaj gelmedi');

  const handleChildClick = (message) => {
    setReceivedMessage(message);
    Alert.alert('Message', `Message from child component: ${message}`);
  };

  return (
    <SafeAreaView style={styles.container}>
      <Text style={styles.title}>Default Props & Parent-Child</Text>

      <Greeting name="John" age={25} />
      <Greeting name="Jane" />
      <Greeting />

      <ChildComponent onButtonClick={handleChildClick} />

      <Text style={styles.statusText}>Son Gelen Mesaj: {receivedMessage}</Text>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 20, justifyContent: 'center', backgroundColor: '#f8fafc' },
  title: { fontSize: 22, fontWeight: 'bold', textAlign: 'center', marginBottom: 20, color: '#0f172a' },
  card: {
    backgroundColor: '#ffffff',
    padding: 14,
    borderRadius: 10,
    marginBottom: 10,
    borderLeftWidth: 4,
    borderLeftColor: '#2563eb',
  },
  greetingText: { fontSize: 16, color: '#1e293b', fontWeight: '600' },
  button: {
    backgroundColor: '#2563eb',
    padding: 15,
    borderRadius: 10,
    alignItems: 'center',
    marginTop: 14,
  },
  buttonText: { color: '#ffffff', fontSize: 16, fontWeight: 'bold' },
  statusText: { marginTop: 16, textAlign: 'center', fontSize: 15, color: '#16a34a', fontWeight: '600' },
});
```

---

## 4️⃣ HAFTA 3 (W3) — Hocanın Koşullu Render (Giriş/Çıkış, Rol/Onay, Stok ve Kategori Filtreleme) Kodu (Snack Expo Uyumlu)

* **Hafta ve Konu Başlığı:** Hafta 3 (W3) · `W3 / 07-conditional-rendering-example.jsx` · **`BasicConditional`, `MultipleConditions`, `ConditionalList`**
* **Bu Kod Ne İşe Yarar?**
  * Hocanın W3 haftasındaki 3 önemli koşullu görünüm örneğini Snack Expo'da doğrudan çalışacak şekilde birleştirir:
    1. **Login / Logout (`isLoggedIn`)**: Giriş yapıldıysa kullanıcı adını ve e-postasını, yapılmadıysa `'Please log in'` uyarısını gösterir.
    2. **Kullanıcı Rolü (`guest`, `user`, `admin`) ve Doğrulama (`isVerified`)**: Seçilen role ve onay durumuna göre farklı panel mesajı gösterir.
    3. **Stoktaki Ürünler (`showOnlyInStock`) ve Kategori (`all`, `fruit`, `vegetable`)**: Ürün listesini hem stok durumuna (`✅` / `❌`) hem de meyve/sebze kategorisine göre filtreler.

```jsx
import React, { useState } from 'react';
import { SafeAreaView, ScrollView, View, Text, TouchableOpacity, StyleSheet } from 'react-native';

const INITIAL_ITEMS = [
  { id: 1, name: 'Apple', category: 'fruit', inStock: true },
  { id: 2, name: 'Carrot', category: 'vegetable', inStock: false },
  { id: 3, name: 'Banana', category: 'fruit', inStock: true },
  { id: 4, name: 'Broccoli', category: 'vegetable', inStock: true },
];

export default function W3ConditionalRenderingExpo() {
  const [isLoggedIn, setIsLoggedIn] = useState(false);
  const [userType, setUserType] = useState('guest');
  const [isVerified, setIsVerified] = useState(false);
  const [showOnlyInStock, setShowOnlyInStock] = useState(false);
  const [selectedCategory, setSelectedCategory] = useState('all');

  const user = { name: 'John Doe', email: 'john@example.com' };

  const renderRoleContent = () => {
    if (userType === 'admin') {
      return 'Admin Panel: Full access to all features';
    } else if (userType === 'user' && isVerified) {
      return 'User Dashboard: Access to user features';
    } else if (userType === 'user' && !isVerified) {
      return 'Please verify your email: Check your inbox';
    } else {
      return 'Guest Access: Limited features available';
    }
  };

  const filteredItems = INITIAL_ITEMS.filter((item) => {
    if (showOnlyInStock && !item.inStock) return false;
    if (selectedCategory !== 'all' && item.category !== selectedCategory) return false;
    return true;
  });

  return (
    <SafeAreaView style={styles.safeArea}>
      <ScrollView contentContainerStyle={styles.container}>
        <View style={styles.card}>
          <Text style={styles.cardTitle}>1. Login / Logout (BasicConditional)</Text>
          <TouchableOpacity
            style={[styles.btn, { backgroundColor: isLoggedIn ? '#dc2626' : '#2563eb' }]}
            onPress={() => setIsLoggedIn(!isLoggedIn)}
          >
            <Text style={styles.btnText}>{isLoggedIn ? 'Logout' : 'Login'}</Text>
          </TouchableOpacity>

          {isLoggedIn ? (
            <View style={styles.statusBox}>
              <Text style={styles.boldText}>Welcome back, {user.name}!</Text>
              <Text style={styles.subText}>Email: {user.email}</Text>
            </View>
          ) : (
            <View style={styles.statusBox}>
              <Text style={styles.boldText}>Please log in</Text>
              <Text style={styles.subText}>You need to be logged in to view this content.</Text>
            </View>
          )}
        </View>

        <View style={styles.card}>
          <Text style={styles.cardTitle}>2. User Role & Verified (MultipleConditions)</Text>
          <View style={styles.row}>
            {['guest', 'user', 'admin'].map((role) => (
              <TouchableOpacity
                key={role}
                style={[styles.pill, userType === role && styles.activePill]}
                onPress={() => setUserType(role)}
              >
                <Text style={[styles.pillText, userType === role && styles.activePillText]}>
                  {role.toUpperCase()}
                </Text>
              </TouchableOpacity>
            ))}
          </View>

          <TouchableOpacity
            style={[styles.btn, { backgroundColor: isVerified ? '#16a34a' : '#64748b' }]}
            onPress={() => setIsVerified(!isVerified)}
          >
            <Text style={styles.btnText}>
              Verified: {isVerified ? 'YES ✓' : 'NO ✗'}
            </Text>
          </TouchableOpacity>

          <Text style={styles.roleResult}>{renderRoleContent()}</Text>
        </View>

        <View style={styles.card}>
          <Text style={styles.cardTitle}>3. Stok ve Kategori Filtresi (ConditionalList)</Text>
          <TouchableOpacity
            style={[styles.btn, { backgroundColor: showOnlyInStock ? '#16a34a' : '#475569' }]}
            onPress={() => setShowOnlyInStock(!showOnlyInStock)}
          >
            <Text style={styles.btnText}>
              {showOnlyInStock ? 'Sadece Stoktakiler Gösteriliyor ✓' : 'Tüm Ürünler Gösteriliyor'}
            </Text>
          </TouchableOpacity>

          <View style={styles.row}>
            {['all', 'fruit', 'vegetable'].map((cat) => (
              <TouchableOpacity
                key={cat}
                style={[styles.pill, selectedCategory === cat && styles.activePill]}
                onPress={() => setSelectedCategory(cat)}
              >
                <Text style={[styles.pillText, selectedCategory === cat && styles.activePillText]}>
                  {cat}
                </Text>
              </TouchableOpacity>
            ))}
          </View>

          {filteredItems.map((item) => (
            <View key={item.id} style={styles.itemRow}>
              <Text style={styles.itemText}>
                {item.name} ({item.category})
              </Text>
              <Text style={{ fontSize: 16 }}>{item.inStock ? '✅ Stokta' : '❌ Tükendi'}</Text>
            </View>
          ))}
        </View>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  safeArea: { flex: 1, backgroundColor: '#f1f5f9' },
  container: { padding: 16, gap: 16 },
  card: { backgroundColor: '#ffffff', padding: 16, borderRadius: 14, gap: 10 },
  cardTitle: { fontSize: 17, fontWeight: 'bold', color: '#0f172a' },
  btn: { paddingVertical: 10, borderRadius: 8, alignItems: 'center' },
  btnText: { color: '#ffffff', fontWeight: 'bold' },
  statusBox: { backgroundColor: '#f8fafc', padding: 12, borderRadius: 8 },
  boldText: { fontSize: 15, fontWeight: 'bold', color: '#1e293b' },
  subText: { fontSize: 13, color: '#64748b', marginTop: 2 },
  row: { flexDirection: 'row', gap: 8 },
  pill: { flex: 1, paddingVertical: 8, borderRadius: 20, backgroundColor: '#e2e8f0', alignItems: 'center' },
  activePill: { backgroundColor: '#2563eb' },
  pillText: { color: '#334155', fontWeight: '600', fontSize: 12 },
  activePillText: { color: '#ffffff' },
  roleResult: { fontSize: 14, fontWeight: 'bold', color: '#2563eb', textAlign: 'center', marginTop: 4 },
  itemRow: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    paddingVertical: 8,
    borderBottomWidth: 1,
    borderBottomColor: '#f1f5f9',
  },
  itemText: { fontSize: 15, color: '#0f172a', fontWeight: '500' },
});
```

---

## 5️⃣ HAFTA 3 (W3) — Hocanın Yapılacaklar Listesi (Todo List — Ekle, Üstünü Çiz, Sil, Filtrele) Kodu (Snack Expo Uyumlu)

* **Hafta ve Konu Başlığı:** Hafta 3 (W3) · `W3 / 08-list-rendering-example.jsx` (`TodoList`) & `W3 / 10-data-sharing-example.jsx` (`TodoApp`)
* **Bu Kod Ne İşe Yarar?**
  * Yeni görev ekler (`ADD_TODO`), göreve tıklayınca tamamlandı işaretleyip yazının üstünü çizer (`textDecorationLine: 'line-through'`), `Sil` butonuyla görevi listeden siler ve `All / Active / Completed` butonlarıyla filtreler.

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

const INITIAL_TODOS = [
  { id: '1', text: 'Learn React Native', completed: false },
  { id: '2', text: 'Build a Snack Expo project', completed: false },
  { id: '3', text: 'Prepare for Exam', completed: true },
];

export default function TodoAppExpo() {
  const [todos, setTodos] = useState(INITIAL_TODOS);
  const [inputValue, setInputValue] = useState('');
  const [filter, setFilter] = useState('all');

  const addTodo = () => {
    if (inputValue.trim() === '') return;
    setTodos((prev) => [
      ...prev,
      { id: String(Date.now()), text: inputValue.trim(), completed: false },
    ]);
    setInputValue('');
  };

  const toggleTodo = (id) => {
    setTodos((prev) =>
      prev.map((todo) =>
        todo.id === id ? { ...todo, completed: !todo.completed } : todo
      )
    );
  };

  const deleteTodo = (id) => {
    setTodos((prev) => prev.filter((todo) => todo.id !== id));
  };

  const filteredTodos = todos.filter((todo) => {
    if (filter === 'completed') return todo.completed;
    if (filter === 'active') return !todo.completed;
    return true;
  });

  return (
    <SafeAreaView style={styles.safeArea}>
      <View style={styles.container}>
        <Text style={styles.title}>Todo List (Ekle · Çiz · Sil · Filtrele)</Text>

        <View style={styles.inputRow}>
          <TextInput
            style={styles.input}
            placeholder="Yeni görev yazın..."
            value={inputValue}
            onChangeText={setInputValue}
          />
          <TouchableOpacity style={styles.addBtn} onPress={addTodo}>
            <Text style={styles.btnText}>Ekle</Text>
          </TouchableOpacity>
        </View>

        <View style={styles.filterRow}>
          {['all', 'active', 'completed'].map((f) => (
            <TouchableOpacity
              key={f}
              style={[styles.filterBtn, filter === f && styles.activeFilterBtn]}
              onPress={() => setFilter(f)}
            >
              <Text style={[styles.filterText, filter === f && styles.activeFilterText]}>
                {f.toUpperCase()}
              </Text>
            </TouchableOpacity>
          ))}
        </View>

        <FlatList
          data={filteredTodos}
          keyExtractor={(item) => item.id}
          contentContainerStyle={{ gap: 10 }}
          renderItem={({ item }) => (
            <View
              style={[
                styles.todoCard,
                { backgroundColor: item.completed ? '#dcfce7' : '#ffffff' },
              ]}
            >
              <TouchableOpacity
                style={{ flex: 1 }}
                onPress={() => toggleTodo(item.id)}
              >
                <Text
                  style={[
                    styles.todoText,
                    {
                      textDecorationLine: item.completed ? 'line-through' : 'none',
                      color: item.completed ? '#166534' : '#0f172a',
                    },
                  ]}
                >
                  {item.completed ? '✓ ' : '○ '}
                  {item.text}
                </Text>
              </TouchableOpacity>

              <TouchableOpacity
                style={styles.deleteBtn}
                onPress={() => deleteTodo(item.id)}
              >
                <Text style={styles.deleteText}>Sil</Text>
              </TouchableOpacity>
            </View>
          )}
        />
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  safeArea: { flex: 1, backgroundColor: '#f8fafc' },
  container: { flex: 1, padding: 20 },
  title: { fontSize: 20, fontWeight: 'bold', color: '#0f172a', marginBottom: 14, textAlign: 'center' },
  inputRow: { flexDirection: 'row', gap: 8, marginBottom: 12 },
  input: {
    flex: 1,
    backgroundColor: '#ffffff',
    borderWidth: 1,
    borderColor: '#cbd5e1',
    borderRadius: 10,
    paddingHorizontal: 12,
    paddingVertical: 10,
    fontSize: 15,
  },
  addBtn: { backgroundColor: '#2563eb', paddingHorizontal: 20, justifyContent: 'center', borderRadius: 10 },
  btnText: { color: '#ffffff', fontWeight: 'bold' },
  filterRow: { flexDirection: 'row', gap: 8, marginBottom: 14 },
  filterBtn: { flex: 1, paddingVertical: 8, borderRadius: 8, backgroundColor: '#e2e8f0', alignItems: 'center' },
  activeFilterBtn: { backgroundColor: '#0f172a' },
  filterText: { color: '#334155', fontWeight: 'bold', fontSize: 12 },
  activeFilterText: { color: '#ffffff' },
  todoCard: {
    flexDirection: 'row',
    alignItems: 'center',
    justifyContent: 'space-between',
    padding: 14,
    borderRadius: 12,
    borderWidth: 1,
    borderColor: '#cbd5e1',
  },
  todoText: { fontSize: 16, fontWeight: '600' },
  deleteBtn: { backgroundColor: '#dc2626', paddingVertical: 6, paddingHorizontal: 12, borderRadius: 6 },
  deleteText: { color: '#ffffff', fontWeight: 'bold', fontSize: 13 },
});
```

---

## 6️⃣ HAFTA 2 (W2) — Hocanın Hava Durumu Kıyafet & Aktivite Önerisi ve Vergi Hesaplama Kodları (Snack Expo Uyumlu)

* **Hafta ve Konu Başlığı:** Hafta 2 (W2) · `W2 / topics / 06_control_flow.js` & `08_functions.js`
* **Bu Kod Ne İşe Yarar?**
  * Hocanın W2 haftasında işlediği **Hava Durumu Seçimine Göre Kıyafet ve Aktivite Önerisi (`sunny`, `rainy`, `windy`, `snowy`)** ile **Gelir ve Vergi Oranı Hesaplama (`calculateTax`)** örneklerinin Snack Expo'da çalışan React Native versiyonudur.

```jsx
import React, { useState } from 'react';
import { SafeAreaView, ScrollView, View, Text, TextInput, TouchableOpacity, StyleSheet } from 'react-native';

const WEATHER_TYPES = [
  { key: 'sunny', label: '☀️ Sunny', color: '#f59e0b', bg: '#fef3c7' },
  { key: 'rainy', label: '🌧️ Rainy', color: '#2563eb', bg: '#dbeafe' },
  { key: 'windy', label: '💨 Windy', color: '#0d9488', bg: '#ccfbf1' },
  { key: 'snowy', label: '❄️ Snowy', color: '#6366f1', bg: '#e0e7ff' },
];

export default function W2WeatherAndTaxApp() {
  const [weather, setWeather] = useState('sunny');
  const [income, setIncome] = useState('10000');
  const [rate, setRate] = useState('20');

  const getOutfit = (condition) => {
    if (condition === 'sunny') return 'Wear sunglasses and light layers.';
    if (condition === 'rainy') return 'Grab a waterproof jacket and boots.';
    if (condition === 'windy') return 'Layer up with a windbreaker.';
    return 'Bundle up with a warm coat and gloves.';
  };

  const getSuggestedActivity = (condition) => {
    switch (condition) {
      case 'sunny':
        return 'Go for a walk or have a picnic.';
      case 'rainy':
        return 'Enjoy a book indoors.';
      case 'windy':
        return 'Fly a kite if you have one.';
      case 'snowy':
        return 'Build a snowman or stay cozy inside.';
      default:
        return 'Make a warm drink and relax.';
    }
  };

  const activeWeather = WEATHER_TYPES.find((w) => w.key === weather) || WEATHER_TYPES[0];
  const numericIncome = Number(income) || 0;
  const numericRate = Number(rate) || 0;
  const taxDue = numericIncome * (numericRate / 100);

  return (
    <SafeAreaView style={styles.safeArea}>
      <ScrollView contentContainerStyle={styles.container}>
        <View style={[styles.card, { backgroundColor: activeWeather.bg, borderColor: activeWeather.color }]}>
          <Text style={[styles.title, { color: activeWeather.color }]}>
            W2 Control Flow: Hava Durumu Önerisi
          </Text>

          <View style={styles.row}>
            {WEATHER_TYPES.map((item) => (
              <TouchableOpacity
                key={item.key}
                style={[
                  styles.weatherBtn,
                  { backgroundColor: weather === item.key ? item.color : '#ffffff' },
                ]}
                onPress={() => setWeather(item.key)}
              >
                <Text
                  style={{
                    color: weather === item.key ? '#ffffff' : '#334155',
                    fontWeight: 'bold',
                    fontSize: 12,
                  }}
                >
                  {item.label}
                </Text>
              </TouchableOpacity>
            ))}
          </View>

          <Text style={styles.resultTitle}>Outfit Recommendation:</Text>
          <Text style={styles.resultBody}>{getOutfit(weather)}</Text>

          <Text style={styles.resultTitle}>Suggested Activity:</Text>
          <Text style={styles.resultBody}>{getSuggestedActivity(weather)}</Text>
        </View>

        <View style={styles.card}>
          <Text style={styles.title}>W2 Functions: Vergi Hesaplayıcı (calculateTax)</Text>
          <TextInput
            style={styles.input}
            placeholder="Gelir (Income)"
            keyboardType="numeric"
            value={income}
            onChangeText={setIncome}
          />
          <TextInput
            style={styles.input}
            placeholder="Vergi Oranı % (Tax Rate)"
            keyboardType="numeric"
            value={rate}
            onChangeText={setRate}
          />
          <View style={styles.taxSummary}>
            <Text style={styles.taxLine}>Gelir (Income): {numericIncome.toFixed(2)} TL</Text>
            <Text style={styles.taxLine}>Vergi Oranı (Rate): %{numericRate}</Text>
            <Text style={styles.taxTotal}>Hesaplanan Vergi: {taxDue.toFixed(2)} TL</Text>
          </View>
        </View>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  safeArea: { flex: 1, backgroundColor: '#f8fafc' },
  container: { padding: 20, gap: 20 },
  card: {
    backgroundColor: '#ffffff',
    padding: 18,
    borderRadius: 16,
    borderWidth: 2,
    borderColor: '#cbd5e1',
    gap: 10,
  },
  title: { fontSize: 18, fontWeight: 'bold', color: '#0f172a' },
  row: { flexDirection: 'row', flexWrap: 'wrap', gap: 8 },
  weatherBtn: { flex: 1, paddingVertical: 10, borderRadius: 10, alignItems: 'center', minWidth: 70 },
  resultTitle: { fontSize: 14, fontWeight: 'bold', color: '#334155', marginTop: 4 },
  resultBody: { fontSize: 15, color: '#0f172a' },
  input: {
    borderWidth: 1,
    borderColor: '#cbd5e1',
    borderRadius: 10,
    padding: 12,
    fontSize: 15,
    backgroundColor: '#f8fafc',
  },
  taxSummary: { backgroundColor: '#eff6ff', padding: 14, borderRadius: 10, gap: 4 },
  taxLine: { fontSize: 14, color: '#1e3a8a' },
  taxTotal: { fontSize: 18, fontWeight: 'bold', color: '#2563eb', marginTop: 4 },
});
```
