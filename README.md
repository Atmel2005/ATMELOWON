# ATMELOWON — OWON VDS1022 GUI & Logic Analyzer in Rust

## Deutsch

Das Projekt ist eine performante und feature-reiche GUI-Alternative für das USB-Oszilloskop OWON VDS1022, geschrieben in Rust. Neben den klassischen Oszilloskop-Funktionen enthält es einen leistungsstarken Logikanalysator (Logic Analyzer) mit Dekodierung verschiedener Protokolle und WGPU Compute Shader-Unterstützung für hardwarebeschleunigte Darstellung.

### Ausrüstung

- USB-Oszilloskop OWON VDS1022 (2 Kanäle, 25 MHz Bandbreite, 100 MSa/s)
- PC / Laptop mit Windows
- Standard USB-Kabel (für Datenverbindung und Stromversorgung)

### Treiber & Einrichtung

Installiere die Treiber `VDS_USBDRV` auf normalem Weg (über den Treiber-Installer oder den Geräte-Manager in Windows). Dadurch kann die Rust-Bibliothek `rusb` (Libusb) direkt und ohne Verzögerung auf das Gerät zugreifen.

### Hauptfunktionen (Vorteile gegenüber dem Original-Hersteller-Programm)

- **Hochperformante Darstellung & Hohe Bildrate**: Flüssiges Rendering mit hoher Frequenz durch GPU Compute Shader (WGPU) oder schnellen CPU-Fallback.
- **Einstellbare Helligkeit & Nachleuchten**: Regler für Strahlhelligkeit (Beam Intensity) und Gitterhelligkeit (Grid Intensity) sowie echter analoger Persistence-Modus.
- **Offline-Analyse-Integration (Oszi)**: Nahtlose Integration des externen Wellenform-Analysators **Oszi** von Elmue ([GitHub-Link](https://github.com/Elmue/Oszi-Waveform-Analyzer)), der als Plugin genutzt wird. Das Programm erkennt automatisch den Pfad zur mitgelieferten Kopie von Oszi, speichert die Pfadkonfiguration und ermöglicht den Export der erfassten Kurven als CSV-Dateien mit automatischem Start des Analysators zur detaillierten Offline-Auswertung.
- **Integrierter Logikanalysator (im Original nicht vorhanden)** mit Unterstützung für:
  - SPI, I2C, UART (mit automatischer Baudraten-Erkennung), CAN, 1-Wire, Manchester, USB (Full Speed / Low Speed), IR-Fernbedienungen (NEC, RC5 usw.) und Magnetstreifenleser (MagStripe).
- **Drei A/D-Konvertierungsmodi** (um analoge Signale für den Logikanalysator in digitale Kurven zu wandeln):
  - **Threshold**: Schwellwert mit Hysterese zur Vermeidung von Rauschen.
  - **Adaptive**: Automatische Pegelanpassung an 50% der Peak-to-Peak-Amplitude pro Halbperiode (ideal bei DC-Offset-Schwankungen).
  - **Min/Max**: Umschaltung genau an lokalen Spannungsminima und -maxima.
- **Flexibler Speicherpuffer (Memory Window)**: Einstellbare Tiefe des Videopuffers (Verlaufsspeicher) und des Dekoder-Logs von 1 bis 600 Sekunden.
- **Historien-Modus & Player**: Aufzeichnen von Signalen und Abspielen mit einstellbarer FPS im integrierten Player.
- **Kontinuierliche Protokollierung auf Festplatte** für den Logikanalysator mit automatischer Ordnerbereinigung (Pruning bis max. 20 GB).
- **Automatische Messungen**: Frequenz, Periode, Anstiegs-/Abfallzeiten, Pulsbreiten, Duty Cycle, Vpp, RMS, Vmax, Vmin, Vavg usw.
- **FFT-Spektrumanalyse** zur Frequenzbereichsanalyse.
- **Firmware-Manager**: Erkennt automatisch die VFPGA-Version des Geräts und lädt fehlende FPGA-Firmware direkt von GitHub herunter.

### Nutzung

1. Schließe das OWON VDS1022 per USB an deinen PC an.
2. Stelle sicher, dass die `VDS_USBDRV`-Treiber installiert sind.
3. Starte die Anwendung über die ausführbare Datei (z. B. `ATMELOWON.exe`).
4. Das Programm lädt automatisch die FPGA-Firmware hoch, initialisiert das Gerät und startet den Datenstrom.

---

## Українська

Проєкт є високопродуктивною та багатофункціональною альтернативою офіційного ПЗ для USB-осцилографа OWON VDS1022. Програма написана на Rust. Окрім класичних функцій осцилографа, вона містить потужний логічний аналізатор з декодуванням популярних протоколів та підтримку WGPU Compute Shaders для апаратного прискорення графіки.

### Обладнання

- USB-осцилограф OWON VDS1022 (2 канали, смуга 25 МГц, 100 MSa/s)
- Комп'ютер або ноутбук під керуванням Windows
- Стандартний кабель USB (для передачі даних та живлення)

### Драйвери та налаштування

Встановіть драйвери `VDS_USBDRV` звичайним способом (через інсталятор драйверів або Диспетчер пристроїв у Windows). Це дозволить бібліотеці `rusb` (Libusb) спілкуватися з пристроєм напряму.

### Основні можливості (Переваги порівняно з оригінальним ПЗ)

- **Висока частота оновлення та роздільна здатність**: Плавний рендеринг сигналів із високим FPS завдяки обчислюваням GPU Compute Shaders (`wgpu`) або оптимізованому CPU-рендереру.
- **Регулювання яскравості та післясвітіння**: Повзунки регулювання яскравості променів (Beam) та сітки (Grid), а також режим аналогового накопичення сигналу (Persistence).
- **Інтеграція з офлайн-аналізатором (Oszi)**: Повна сумісність із зовнішнім аналізатором сигналів **Oszi** від автора Elmue ([GitHub](https://github.com/Elmue/Oszi-Waveform-Analyzer)), який використовується як плагін. Програма автоматично знаходить копію Oszi у своїй папці, зберігає шлях у конфігурації та дозволяє одним кліком експортувати поточні осцилограми в CSV з автоматичним запуском Oszi для детального офлайн-аналізу.
- **Вбудований логічний аналізатор (відсутній в оригіналі)** із декодером протоколів:
  - SPI, I2C, UART (з автовизначенням швидкості), CAN, 1-Wire, Manchester, USB (Full Speed / Low Speed), ІЧ-пульти (NEC, RC5 тощо) та магнітні картки (MagStripe).
- **Три алгоритми АЦП** для підготовки аналогових сигналів перед логічним декодуванням:
  - **Threshold**: Поріг із налаштовуваним гістерезисом для захисту від шумів.
  - **Adaptive**: Поріг адаптується под 50% розмаху сигналу для кожного півперіоду (зручно при дрейфі постійної складової).
  - **Min/Max**: Перемикання точно у точках локальних мінімумів та максимумів напруги.
- **Гнучке вікно пам'яті (Відеобуфер)**: Можливість налаштовувати тривалість буфера історії та логування від 1 до 600 секунд.
- **Відтворення історії**: Запис кадрів сигналу та відтворення через вбудований плеєр із вибором швидкості (FPS).
- **Безперервне логування на диск** для логічного аналізатора з автоматичним очищенням старих записів (ліміт папки до 20 ГБ).
- **Автоматичні вимірії**: Частота, період, час наростання/спаду фронтів, шпажність, Vpp, RMS, Vmax, Vmin, Vavg тощо.
- **FFT-аналізатор спектра** для аналізу сигналів у частотній області.
- **Менеджер прошивок**: Автоматично зчитує версію FPGA пристрою та завантажує потрібні прошивки безпосередньо з GitHub.

### Використання

1. Підключіть осцилограф OWON VDS1022 до USB.
2. Перевірте, що встановлено драйвери `VDS_USBDRV`.
3. Запустіть програму за допомогою готового файлу `ATMELOWON.exe`.
4. Програма автоматично розпізнає пристрій, завантажить прошивку FPGA та почне виводити сигнал.

---

## English

The project is a high-performance, feature-rich GUI alternative for the OWON VDS1022 USB oscilloscope, written in Rust. Along with classic oscilloscope functionality, it includes a powerful logic analyzer with protocol decoding and WGPU Compute Shader support for hardware-accelerated waveform rendering.

### Hardware

- OWON VDS1022 USB oscilloscope (2 channels, 25 MHz bandwidth, 100 MSa/s)
- PC / Laptop running Windows
- Standard USB cable (for both data and power)

### Drivers & Setup

Install the `VDS_USBDRV` drivers in the standard way (via the driver installer or Windows Device Manager). This allows the Rust `rusb` (Libusb) library to communicate directly with the hardware.

### Key Features (Advantages over the Original Software)

- **High Refresh Rate & High Resolution**: Smooth, high-FPS waveform rendering powered by GPU Compute Shaders (WGPU) with a fast CPU fallback.
- **Adjustable Brightness & Hysteresis**: Precise sliders for waveform beam brightness (Beam Intensity) and grid brightness (Grid Intensity), combined with an analog-style Persistence mode.
- **Offline Waveform Analyzer Integration (Oszi)**: Built-in support for the external offline waveform analyzer **Oszi** by Elmue ([GitHub](https://github.com/Elmue/Oszi-Waveform-Analyzer)) used as a plugin. The application automatically auto-detects the directory containing the bundled copy of Oszi, saves the configured path, and provides one-click export ("EXPORT OSZI") of captured waveforms as CSV with auto-launching of the analyzer for detailed offline examination.
- **Built-in Logic Analyzer (not available in the original)** with decoding support for:
  - SPI, I2C, UART (with auto-baud rate detection), CAN, 1-Wire, Manchester, USB (Full Speed / Low Speed), IR Remote (NEC, RC5, etc.), and MagStripe (Magnetic Stripe Reader).
- **Three A/D Conversion Algorithms** to translate analog waves into digital logic lines for decoding:
  - **Threshold**: Hysteresis threshold to prevent noise-induced triggering.
  - **Adaptive**: Adapts to 50% of the peak-to-peak amplitude for each half-period (ideal for signals with varying DC offset).
  - **Min/Max**: Transitions state exactly at local voltage minima and maxima.
- **Adjustable Memory Window (Video & Log Buffer)**: Configurable history and decode log buffer depth ranging from 1 to 600 seconds.
- **Waveform History & Player**: Record and play back captured waveforms using a dedicated history player with adjustable speed (FPS).
- **Continuous Disk Logging** for logic analyzer captures with automatic folder size pruning (up to 20 GB).
- **Automatic Measurements**: Frequency, period, rise/fall times, pulse width, duty cycle, peak-to-peak (Vpp), RMS, Vmax, Vmin, Vavg, and more.
- **FFT Spectrum Analysis** to evaluate signals in the frequency domain.
- **Firmware Manager**: Auto-detects the connected device's VFPGA version and fetches the corresponding FPGA binary directly from GitHub.

### Usage

1. Connect the OWON VDS1022 oscilloscope via USB to your PC.
2. Ensure the `VDS_USBDRV` drivers are installed.
3. Launch the application by running the executable file (e.g., `ATMELOWON.exe`).
4. The application will automatically detect the device, load the FPGA firmware, and begin capturing.

---

## Russian

Проект представляет собой высокопроизводительную и функциональную альтернативу официальному ПО для USB-осциллографа OWON VDS1022, написанную на Rust. Помимо стандартного режима осциллографа, приложение содержит полноценный логический анализатор с декодером популярных протоколов и поддержку WGPU Compute Shaders для аппаратного ускорения графики.

### Аппаратная часть

- USB-осциллограф OWON VDS1022 (2 канала, полоса 25 МГц, 100 MSa/s)
- Компьютер или ноутбук под управлением Windows
- Стандартный кабель USB (для передачи данных и питания)

### Драйверы и настройка

Установите драйверы `VDS_USBDRV` обычным способом (через установщик драйверов или Диспетчер устройств в Windows). Это позволит Rust-библиотеке `rusb` (Libusb) работать с устройством напрямую.

### Основные возможности (Преимущества по сравнению с оригинальным ПО)

- **Высокая частота обновления и разрешение**: Плавная отрисовка осциллограмм с высоким FPS благодаря GPU Compute Shaders (WGPU) или оптимизированному CPU-рендереру.
- **Регулировка яркости и послесвечения**: Ползунки регулировки яркости лучей (Beam) и сетки (Grid), а также режим аналогового послесвечения (Persistence).
- **Интеграция с офлайн-анализатором (Oszi)**: Бесшовная совместимость с внешним анализатором осциллограмм **Oszi** от автора Elmue ([GitHub](https://github.com/Elmue/Oszi-Waveform-Analyzer)), который используется как плагин. Программа автоматически находит копию Oszi в рабочей папке, сохраняет путь в конфигурационном файле и позволяет одним нажатием экспортировать буфер в CSV с автоматическим запуском Oszi для детального офлайн-анализа.
- **Встроенный логический анализатор (отсутствует в оригинале)** с декодированием протоколов:
  - SPI, I2C, UART (с автоопределением скорости), CAN, 1-Wire, Manchester, USB (Full Speed / Low Speed), ИК-пульты (NEC, RC5 и др.) и магнитные ленты (MagStripe).
- **Три режима АЦП** для преобразования аналогового сигнала в цифровую шину перед декодированием:
  - **Threshold**: Порог с настраиваемым гистерезисом для подавления помех.
  - **Adaptive**: Адаптивный порог под 50% размаха сигнала на каждом полупериоде (идеально для сигналов с колеблющимся постоянным смещением).
  - **Min/Max**: Переключение цифрового уровня строго в точках локальных минимумов и максимумов напряжения.
- **Регулируемое окно памяти (Видеобуфер)**: Возможность настраивать глубину буфера истории и декодера от 1 до 600 секунд.
- **Запись и воспроизведение истории**: Буферизация кадров с возможностью воспроизведения через встроенный плеер с выбором скорости (FPS).
- **Непрерывное логирование на диск** для логического анализатора с автоматическим удалением старых файлов (лимит папки до 20 ГБ).
- **Автоматические измерения**: Частота, период, фронты, ширина импульса, скважность, размах (Vpp), RMS, Vmax, Vmin, Vavg и т.д.
- **FFT-анализ спектра** для исследования сигналов в частотной области.
- **Менеджер прошивок**: Автоматически считывает версию FPGA прибора и скачивает подходящий файл прошивки прямо из репозитория GitHub при её отсутствии.

### Использование

1. Подключите осциллограф OWON VDS1022 к USB-порту вашего ПК.
2. Убедитесь, что установлены драйверы `VDS_USBDRV`.
3. Запустите приложение с помощью готового исполняемого файла (например, `ATMELOWON.exe`).
4. Программа сама распознает устройство, загрузит прошивку FPGA на прибор и начнет прием данных.
