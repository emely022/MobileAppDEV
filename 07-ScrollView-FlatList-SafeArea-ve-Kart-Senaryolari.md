# 📜 ScrollView (Yatay/Dikey), FlatList, SafeAreaView, Onboarding ve Dashboard Kart Senaryoları

> **[⬅️ Ana Sınav Rehberine (README) Dön](./README.md)**

![ScrollView, FlatList ve SafeAreaView Görsel Rehberi](./gorseller/07-scrollview-flatlist-safearea.svg)

---

## 📌 Bu Dosya Hangi Hafta ve Hangi Ders Kodlarına Karşılık Gelir?

| Hafta | Ders Notu Dosyası ve Konu Başlığı | Hocanın Kodundaki Bileşen Adı | Ne İşe Yarar? |
| :--- | :--- | :--- | :--- |
| **Hafta 6 (W6)** | `W6 / components / ScrollView.md` — **Example 2: Weekly Schedule Horizontal Scroll** | `WeeklySchedule` | `ScrollView horizontal` kullanarak Pazartesi–Cuma çalışma planı kartlarını yan yana yatay kaydırılabilir şekilde gösterir. |
| **Hafta 6 (W6)** | `W6 / components / ScrollView.md` — **Example 1: Terms of Service with Confirmation Button** | `TermsAgreement` | Uzun sözleşme metnini en alta kadar kaydırınca (`onScroll`) alttaki `Accept terms` butonunu aktif hale getirir. |
| **Hafta 4 (W4)** | `W4 / 7-example-basic-components.md` — **4. ScrollView - Scrollable Container** | `ScrollViewExamples` | 20 adet gölgeli beyaz kartı (`Item 1` ... `Item 20`) dikey `ScrollView` içinde listeler. |
| **Hafta 6 (W6)** | `W6 / components / SafeAreaView.md` — **Example 1: Onboarding Screen** | `OnboardingScreen` | `Step 1 / 3` şeklinde adım adım ilerleyen tanıtım ekranı; son adımda buton mavi (`#38bdf8`) renkten yeşile (`#22c55e`) ve `Continue` yazısından `Restart` yazısına dönüşür. |
| **Hafta 6 (W6)** | `W6 / components / SafeAreaView.md` — **Example 2: SafeAreaProvider Notched Header** | `NotchedHeaderDemo` | Üstte yuvarlak profil fotoğrafı ve `Instructor Dashboard` başlığı bulunan güvenli alan (`useSafeAreaInsets`) ekranı. |
| **Hafta 6 (W6)** | `W6 / components / View.md` — **Example 1: Dashboard Card with Stats** | `DashboardCard` | `Daily Lesson Progress`, `+12%`, `width: '65%'` ilerleme çubuğu ve `13 / 20` istatistiklerini içeren dashboard kartı. |
| **Hafta 6 (W6)** | `W6 / components / View.md` — **Example 2: Responsive Grid with onLayout** | `ResponsiveGrid` | Ekran genişliğine göre (`onLayout`) satır başına 2 veya 3 kart dizen ızgara görünümü. |
| **Hafta 6 (W6)** | `W6 / components / FlatList.md` — **Example 2: Infinite Scroll with Pull-to-Refresh** | `InfiniteNotes` | Aşağı çekerek yenileme (`RefreshControl`) ve listenin sonuna gelince yeni veri yükleme (`onEndReached`) örneği. |

---

## ⚡ Sınavda Hoca Kaydırma, İlerleme Çubuğu veya Adım Ekranı Değiştirirse Nereyi Değiştireceksin?

| Hocanın Görselde İstediği Değişiklik | Kodda Değiştireceğin Satır |
| :--- | :--- |
| Dikey `ScrollView`'u **Yatay Kaydırmalı** yapmak | `<ScrollView horizontal={true} showsHorizontalScrollIndicator={false}>` |
| Yatay `ScrollView`'u **Dikey Kaydırmalı** yapmak | `horizontal` prop'unu sil ve kartların `width: 220` değerini `'100%'` yap |
| `DashboardCard` içindeki **İlerleme Çubuğu Doluluk Oranını** değiştirmek | İçteki `View` stilinde `width: '65%'` değerini örn. `'85%'` yap |
| `OnboardingScreen` içine **4. Adım** eklemek | `STEPS` dizisine yeni bir `{ title: '...', description: '...' }` objesi ekle |
| `OnboardingScreen`'e **Geri (Previous) Butonu** eklemek | `setStep((prev) => Math.max(0, prev - 1))` çalıştıran ikinci bir buton ekle |

---

## 1️⃣ HAFTA 6 (W6) — Hocanın Orijinal Yatay Kaydırmalı Haftalık Plan Kodu (`WeeklySchedule`)

* **Hafta ve Konu Başlığı:** Hafta 6 (W6) · `W6 / components / ScrollView.md` · **Example 2: Weekly Schedule Horizontal Scroll (`WeeklySchedule`)**
* **Bu Kod Ne İşe Yarar?**
  * `ScrollView` bileşenine `horizontal` prop'u vererek içindeki 5 gün kartını (`Monday` – `Friday`) yan yana yatay kaydırılabilir şekilde dizer.

```jsx
import React from 'react';
import { SafeAreaView, ScrollView, Text, View } from 'react-native';

const WEEKLY_PLAN = [
  { day: 'Monday', topic: 'Kickoff Session', duration: '40 min' },
  { day: 'Tuesday', topic: 'Core Components', duration: '60 min' },
  { day: 'Wednesday', topic: 'Navigation', duration: '50 min' },
  { day: 'Thursday', topic: 'State Management', duration: '55 min' },
  { day: 'Friday', topic: 'Performance', duration: '45 min' },
];

export default function WeeklySchedule() {
  return (
    <SafeAreaView style={{ flex: 1, backgroundColor: '#0f172a' }}>
      <View style={{ paddingVertical: 32 }}>
        <Text
          style={{
            fontSize: 22,
            fontWeight: '700',
            marginLeft: 24,
            color: '#f8fafc',
          }}
        >
          Weekly Study Plan
        </Text>
        <ScrollView
          horizontal
          showsHorizontalScrollIndicator={false}
          contentContainerStyle={{ paddingHorizontal: 24, paddingTop: 16, gap: 16 }}
        >
          {WEEKLY_PLAN.map((item) => (
            <View
              key={item.day}
              style={{
                width: 220,
                padding: 20,
                borderRadius: 20,
                backgroundColor: '#1f2937',
                justifyContent: 'center',
                gap: 10,
              }}
            >
              <Text style={{ color: '#cbd5f5', fontSize: 16 }}>
                {item.day}
              </Text>
              <Text
                style={{ color: '#f1f5f9', fontWeight: '600', fontSize: 20 }}
              >
                {item.topic}
              </Text>
              <Text style={{ color: '#94a3b8' }}>{item.duration}</Text>
            </View>
          ))}
        </ScrollView>
      </View>
    </SafeAreaView>
  );
}
```

---

## 2️⃣ HAFTA 6 (W6) — Hocanın Orijinal En Alta Kaydırınca Aktifleşen Sözleşme Onay Kodu (`TermsAgreement`)

* **Hafta ve Konu Başlığı:** Hafta 6 (W6) · `W6 / components / ScrollView.md` · **Example 1: Terms of Service with Confirmation Button (`TermsAgreement`)**
* **Bu Kod Ne İşe Yarar?**
  * Kullanıcı sözleşme metnini en alta kadar kaydırdığında `handleScroll` fonksiyonu `reachedEnd` state'ini `true` yapar.
  * En alta inmeden önce buton pasiftir (`disabled`) ve üzerinde `'Scroll to the bottom to continue'` yazar; en alta inince `'Accept terms'` olur; tıklandığında ise yeşil (`#22c55e`) olup `'Accepted'` yazar.

```jsx
import React, { useRef, useState } from 'react';
import { Button, SafeAreaView, ScrollView, Text, View } from 'react-native';

const TERMS = `${'Terms of service '.repeat(120)}\n\nPlease confirm that you have read the agreement.`;

export default function TermsAgreement() {
  const [accepted, setAccepted] = useState(false);
  const [reachedEnd, setReachedEnd] = useState(false);
  const scrollViewRef = useRef(null);
  const requestedPosition = useRef(false);

  const handleScroll = (event) => {
    const { layoutMeasurement, contentOffset, contentSize } =
      event.nativeEvent;
    const scrolledToBottom =
      layoutMeasurement.height + contentOffset.y >= contentSize.height - 20;
    if (scrolledToBottom && !reachedEnd) {
      setReachedEnd(true);
    }
  };

  return (
    <SafeAreaView style={{ flex: 1, backgroundColor: '#e2e8f0' }}>
      <View style={{ flex: 1, padding: 24, gap: 16 }}>
        <Text style={{ fontSize: 22, fontWeight: '700', color: '#0f172a' }}>
          Terms of Service
        </Text>
        <ScrollView
          ref={scrollViewRef}
          onScroll={handleScroll}
          scrollEventThrottle={16}
          contentContainerStyle={{
            padding: 18,
            backgroundColor: '#fff',
            borderRadius: 16,
            gap: 12,
            minHeight: 400,
          }}
          onContentSizeChange={() => {
            if (!requestedPosition.current && scrollViewRef.current) {
              requestedPosition.current = true;
              scrollViewRef.current.scrollTo({ y: 0, animated: false });
            }
          }}
          nestedScrollEnabled
        >
          <Text style={{ lineHeight: 22, color: '#334155' }}>{TERMS}</Text>
        </ScrollView>
        <View style={{ marginTop: 8, marginBottom: 32 }}>
          <Button
            title={
              reachedEnd
                ? accepted
                  ? 'Accepted'
                  : 'Accept terms'
                : 'Scroll to the bottom to continue'
            }
            disabled={!reachedEnd || accepted}
            onPress={() => setAccepted(true)}
            color={accepted ? '#22c55e' : '#2563eb'}
          />
        </View>
      </View>
    </SafeAreaView>
  );
}
```

---

## 3️⃣ HAFTA 6 (W6) — Hocanın Orijinal Adım Adım Tanıtım Ekranı Kodu (`OnboardingScreen`)

* **Hafta ve Konu Başlığı:** Hafta 6 (W6) · `W6 / components / SafeAreaView.md` · **Example 1: Onboarding Screen (`OnboardingScreen`)**
* **Bu Kod Ne İşe Yarar?**
  * `STEPS` dizisindeki 3 adımı sırasıyla gösterir (`Step 1 / 3`, `Step 2 / 3`, `Step 3 / 3`).
  * İlk iki adımda buton mavi (`#38bdf8`) ve yazısı `'Continue'` iken, son adımda (`lastStep`) buton yeşile (`#22c55e`) ve yazısı `'Restart'`a dönüşür; tıklandığında `setStep(0)` ile başa döner.

```jsx
import React, { useState } from 'react';
import {
  SafeAreaView,
  StatusBar,
  Text,
  TouchableOpacity,
  View,
} from 'react-native';

const STEPS = [
  {
    title: 'Welcome to the React Native Course',
    description:
      'You will learn core components, navigation, and state management step by step.',
  },
  {
    title: 'Discover Core Components',
    description:
      'Practice building layouts with View, Text, Image, and more.',
  },
  {
    title: 'Kick Off with Expo',
    description:
      'Run expo start to launch the project and test on your device in real time.',
  },
];

export default function OnboardingScreen() {
  const [step, setStep] = useState(0);
  const lastStep = step === STEPS.length - 1;

  const handleNext = () => {
    if (lastStep) {
      setStep(0);
      return;
    }
    setStep((prev) => prev + 1);
  };

  return (
    <SafeAreaView style={{ flex: 1, backgroundColor: '#0f172a' }}>
      <StatusBar barStyle="light-content" />
      <View style={{ flex: 1, justifyContent: 'space-between', padding: 24 }}>
        <View style={{ gap: 16 }}>
          <Text style={{ color: '#38bdf8', fontSize: 16, fontWeight: '600' }}>
            Step {step + 1} / {STEPS.length}
          </Text>
          <Text style={{ color: '#f8fafc', fontSize: 30, fontWeight: '700' }}>
            {STEPS[step].title}
          </Text>
          <Text style={{ color: '#cbd5f5', lineHeight: 22 }}>
            {STEPS[step].description}
          </Text>
        </View>
        <View style={{ gap: 12 }}>
          {lastStep && (
            <Text style={{ color: '#94a3b8', textAlign: 'center' }}>
              You’re ready! Restart the flow any time you need a refresher.
            </Text>
          )}
          <TouchableOpacity
            onPress={handleNext}
            activeOpacity={0.8}
            style={{
              paddingVertical: 16,
              borderRadius: 12,
              backgroundColor: lastStep ? '#22c55e' : '#38bdf8',
              alignItems: 'center',
            }}
          >
            <Text style={{ color: '#0f172a', fontWeight: '700' }}>
              {lastStep ? 'Restart' : 'Continue'}
            </Text>
          </TouchableOpacity>
        </View>
      </View>
    </SafeAreaView>
  );
}
```

---

## 4️⃣ HAFTA 6 (W6) — Hocanın Orijinal İlerleme Çubuklu Dashboard Kartı ve Responsive Grid Kodları (`DashboardCard` & `ResponsiveGrid`)

### A) `DashboardCard` (`W6 / components / View.md` — Example 1)
* **Bu Kod Ne İşe Yarar?**
  * Üst satırda `flexDirection: 'row', justifyContent: 'space-between'` ile başlığı sola, `+12%` yüzdesini sağa yaslar.
  * Ortada iki iç içe `View` kullanarak `%65` dolu mavi bir ilerleme çubuğu (progress bar) çizer.
  * Alt satırda `Lessons completed` ve `13 / 20` bilgisini iki uca yaslar.

```jsx
import React from 'react';
import { SafeAreaView, View, Text } from 'react-native';

export default function DashboardCard() {
  return (
    <SafeAreaView style={{ flex: 1, backgroundColor: '#020617' }}>
      <View
        style={{
          flex: 1,
          justifyContent: 'center',
          padding: 24,
        }}
      >
        <View
          style={{
            padding: 24,
            borderRadius: 20,
            backgroundColor: '#0f172a',
            gap: 20,
          }}
        >
          <View style={{ flexDirection: 'row', justifyContent: 'space-between' }}>
            <Text style={{ color: '#e2e8f0', fontSize: 18, fontWeight: '600' }}>
              Daily Lesson Progress
            </Text>
            <Text style={{ color: '#38bdf8', fontWeight: '600' }}>+12%</Text>
          </View>
          <View
            style={{
              height: 8,
              borderRadius: 8,
              backgroundColor: '#1e293b',
            }}
          >
            <View
              style={{
                width: '65%',
                height: '100%',
                borderRadius: 8,
                backgroundColor: '#38bdf8',
              }}
            />
          </View>
          <View style={{ flexDirection: 'row', justifyContent: 'space-between' }}>
            <Text style={{ color: '#94a3b8' }}>Lessons completed</Text>
            <Text style={{ color: '#e2e8f0', fontWeight: '600' }}>13 / 20</Text>
          </View>
        </View>
      </View>
    </SafeAreaView>
  );
}
```

### B) `ResponsiveGrid` (`W6 / components / View.md` — Example 2)
* **Bu Kod Ne İşe Yarar?**
  * `COURSES` dizisindeki 6 konuyu `flexDirection: 'row', flexWrap: 'wrap'` ile 2'şerli (ekran genişliği 500'den büyükse 3'erli) kutular halinde ızgara olarak dizer.

```jsx
import React, { useState } from 'react';
import { SafeAreaView, View, Text } from 'react-native';

const COURSES = [
  'Core Components',
  'State Management',
  'Navigation',
  'Performance',
  'Testing',
  'Deployment',
];

export default function ResponsiveGrid() {
  const [cardsPerRow, setCardsPerRow] = useState(2);

  return (
    <SafeAreaView style={{ flex: 1, backgroundColor: '#f8fafc' }}>
      <View
        style={{ flex: 1, padding: 24 }}
        onLayout={(event) => {
          const { width } = event.nativeEvent.layout;
          setCardsPerRow(width > 500 ? 3 : 2);
        }}
      >
        <Text style={{ fontSize: 22, fontWeight: '700', marginBottom: 16 }}>
          Course Topics
        </Text>
        <View
          style={{
            flexDirection: 'row',
            flexWrap: 'wrap',
            gap: 16,
          }}
        >
          {COURSES.map((title) => (
            <View
              key={title}
              style={{
                width: `${100 / cardsPerRow - 4}%`,
                padding: 18,
                borderRadius: 16,
                backgroundColor: '#e2e8f0',
              }}
            >
              <Text style={{ fontWeight: '600', color: '#1f2937' }}>
                {title}
              </Text>
            </View>
          ))}
        </View>
      </View>
    </SafeAreaView>
  );
}
```

---

## 5️⃣ HAFTA 6 (W6) — Hocanın Orijinal Profil Fotoğraflı Üst Başlık Kodu (`NotchedHeaderDemo`)

* **Hafta ve Konu Başlığı:** Hafta 6 (W6) · `W6 / components / SafeAreaView.md` · **Example 2: SafeAreaProvider Notched Header (`NotchedHeaderDemo`)**
* **Bu Kod Ne İşe Yarar?**
  * `react-native-safe-area-context` paketindeki `SafeAreaProvider` ve `useSafeAreaInsets` kancasını kullanır.
  * Ekranın en üstünde sol tarafta `40x40` yuvarlak (`borderRadius: 20`) profil resmi, sağında `Instructor Dashboard` başlığı ve altında ders özet kartı gösterir.

```jsx
import React from 'react';
import {
  SafeAreaProvider,
  SafeAreaView,
  useSafeAreaInsets,
} from 'react-native-safe-area-context';
import { Image, Text, View } from 'react-native';

function HeaderContent() {
  const insets = useSafeAreaInsets();

  return (
    <View style={{ flex: 1, backgroundColor: '#020617' }}>
      <SafeAreaView
        edges={['top']}
        style={{
          backgroundColor: '#0f172a',
          paddingTop: insets.top,
        }}
      >
        <View
          style={{
            paddingHorizontal: 20,
            paddingBottom: 16,
            flexDirection: 'row',
            alignItems: 'center',
            gap: 12,
          }}
        >
          <Image
            source={{
              uri: 'https://avatars.githubusercontent.com/u/499550?v=4',
            }}
            style={{ width: 40, height: 40, borderRadius: 20 }}
          />
          <View style={{ flex: 1 }}>
            <Text style={{ color: '#f8fafc', fontWeight: '700', fontSize: 18 }}>
              Instructor Dashboard
            </Text>
            <Text style={{ color: '#94a3b8' }}>
              Welcome back! Review the highlights before you go live.
            </Text>
          </View>
        </View>
      </SafeAreaView>

      <View style={{ flex: 1, padding: 24, gap: 16 }}>
        <Text style={{ color: '#f8fafc', fontSize: 20, fontWeight: '600' }}>
          Latest Lessons
        </Text>
        <View
          style={{
            borderRadius: 16,
            padding: 20,
            backgroundColor: '#1f2937',
            gap: 12,
          }}
        >
          <Text style={{ color: '#38bdf8', fontWeight: '700' }}>
            1. Core Components
          </Text>
          <Text style={{ color: '#cbd5f5', lineHeight: 20 }}>
            Recap how to structure layouts with View, Text, and Image, backed by practical examples.
          </Text>
        </View>
      </View>
    </View>
  );
}

export default function NotchedHeaderDemo() {
  return (
    <SafeAreaProvider>
      <HeaderContent />
    </SafeAreaProvider>
  );
}
```

---

## 6️⃣ HAFTA 6 (W6) — Hocanın Orijinal Sonsuz Kaydırma ve Yenileme Kodu (`InfiniteNotes`)

* **Hafta ve Konu Başlığı:** Hafta 6 (W6) · `W6 / components / FlatList.md` · **Example 2: Infinite Scroll with Pull-to-Refresh (`InfiniteNotes`)**
* **Bu Kod Ne İşe Yarar?**
  * `FlatList` içinde 6'şar 6'şar ders notu (`Lesson Note #1`, `#2`, ...) yükler.
  * Ekranı yukarıdan aşağı çekince `RefreshControl` ile listeyi sıfırlayıp 1. sayfayı baştan yükler; listenin sonuna doğru kaydırınca `onEndReached` ile yeni 6 not daha ekler.

```jsx
import React, { useCallback, useEffect, useState } from 'react';
import {
  ActivityIndicator,
  FlatList,
  RefreshControl,
  SafeAreaView,
  Text,
  View,
} from 'react-native';

const fetchPage = async (page) => {
  await new Promise((resolve) => setTimeout(resolve, 600));
  return Array.from({ length: 6 }, (_, index) => {
    const id = (page - 1) * 6 + index + 1;
    return { id: String(id), title: `Lesson Note #${id}` };
  });
};

export default function InfiniteNotes() {
  const [notes, setNotes] = useState([]);
  const [page, setPage] = useState(1);
  const [loadingMore, setLoadingMore] = useState(false);
  const [refreshing, setRefreshing] = useState(false);

  const loadPage = useCallback(
    async (pageToLoad, isRefresh = false) => {
      if (loadingMore || refreshing) return;
      if (isRefresh) {
        setRefreshing(true);
      } else {
        setLoadingMore(true);
      }
      const newNotes = await fetchPage(pageToLoad);
      setNotes((prev) => (isRefresh ? newNotes : [...prev, ...newNotes]));
      setPage(pageToLoad + 1);
      setLoadingMore(false);
      setRefreshing(false);
    },
    [loadingMore, refreshing]
  );

  useEffect(() => {
    loadPage(1, true);
  }, [loadPage]);

  return (
    <SafeAreaView style={{ flex: 1, backgroundColor: '#0f172a' }}>
      <FlatList
        data={notes}
        keyExtractor={(item) => item.id}
        contentContainerStyle={{ padding: 24, gap: 16 }}
        renderItem={({ item }) => (
          <View
            style={{
              padding: 18,
              borderRadius: 14,
              backgroundColor: '#1f2937',
            }}
          >
            <Text style={{ fontSize: 16, color: '#f8fafc' }}>{item.title}</Text>
          </View>
        )}
        refreshControl={
          <RefreshControl
            refreshing={refreshing}
            onRefresh={() => loadPage(1, true)}
            tintColor="#38bdf8"
          />
        }
        onEndReached={() => loadPage(page)}
        onEndReachedThreshold={0.4}
        ListFooterComponent={
          loadingMore ? (
            <ActivityIndicator size="small" color="#38bdf8" />
          ) : null
        }
        ListHeaderComponent={() => (
          <Text
            style={{
              fontSize: 22,
              fontWeight: '700',
              color: '#f8fafc',
              marginBottom: 8,
            }}
          >
            Lesson Notes Feed
          </Text>
        )}
      />
    </SafeAreaView>
  );
}
```
