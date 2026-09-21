# CSE457 - Lab 1: Phân tích và xử lý tín hiệu âm thanh số

## Thông tin

- **Học phần:** CSE457 - Xử lý âm thanh và tiếng nói
- **Lab:** Lab 1 - Phân tích và xử lý tín hiệu âm thanh số
- **Sinh viên:** Lê Trọng Huy
- **MSSV:** 2351260658
- **Ngôn ngữ:** Python 3
- **Môi trường:** Jupyter Notebook / VS Code

## Giới thiệu

Repository này chứa bài thực hành Lab 1 của học phần **CSE457 - Xử lý âm thanh và tiếng nói**.

Mục tiêu của Lab là thực hiện pipeline xử lý tín hiệu âm thanh số từ dữ liệu âm thanh đầu vào, bao gồm:

**Audio → biểu diễn số → phân tích miền thời gian → FFT/STFT → lọc số → lượng tử hóa → resampling → mã hóa và đánh giá.**

Các nội dung được triển khai theo yêu cầu của Lab gồm:

- Đọc và kiểm tra thông tin file âm thanh.
- Phân tích tín hiệu trong miền thời gian.
- Phân tích phổ bằng FFT.
- Phân tích thời gian - tần số bằng STFT/Spectrogram.
- So sánh cửa sổ Rectangular và Hamming.
- Thiết kế và áp dụng FIR filter.
- Lượng tử hóa tín hiệu với nhiều mức bit.
- Resampling về 16 kHz và 8 kHz.
- Tính SNR, PCM bitrate, file size và compression ratio.

Nội dung thực hiện
A. Đọc và kiểm tra dữ liệu âm thanh
Chuyển file âm thanh đầu vào sang WAV PCM để thuận tiện cho việc xử lý.
Kiểm tra:
Sampling rate Fs
Số kênh channels
Duration
dtype
Sample width / bit depth
File size
Nếu tín hiệu là stereo, tạo tín hiệu mono bằng cách lấy trung bình hai kênh.
So sánh waveform và RMS giữa các kênh.
Chuẩn hóa tín hiệu về miền [-1, 1].
B. Phân tích miền thời gian
Vẽ waveform của toàn bộ tín hiệu.
Vẽ chi tiết một đoạn tín hiệu từ 0.5 - 1.0 s.
Tính:
Peak
RMS
Energy
Clipping
Chọn ít nhất hai đoạn có đặc tính khác nhau để so sánh.
C. Phân tích miền tần số bằng FFT
Chọn một đoạn tín hiệu tương đối ổn định dài 0.5 - 1 s.
Áp dụng cửa sổ Hamming.
Tính FFT.
Vẽ:
Magnitude spectrum
Spectrum theo dB
Xác định ít nhất 3 đỉnh phổ nổi bật.
Thử nhiều giá trị NFFT.
Tính và so sánh frequency-bin spacing:
Δf = Fs / NFFT
Phân biệt frequency-bin spacing với true frequency resolution.
D. STFT và Spectrogram
Sử dụng cấu hình chuẩn:
Frame ≈ 25 ms
Hop ≈ 10 ms
So sánh ba frame length:
10 ms
25 ms
50 ms
Phân tích:
Vùng năng lượng ổn định.
Transient.
Time resolution.
Frequency resolution.
Trade-off giữa độ phân giải thời gian và tần số.
E. Thí nghiệm cửa sổ

So sánh hai loại cửa sổ trên cùng một đoạn tín hiệu và cùng NFFT:

Rectangular
Hamming

Phân tích:

Main lobe
Side lobe
Spectral leakage

Sử dụng log-spectrum để quan sát rõ sự khác biệt.

F. Lọc số bằng FIR

Thiết kế và áp dụng các bộ lọc FIR:

Low-pass filter.
High-pass filter hoặc Band-pass filter.

Các kết quả bao gồm:

Filter coefficients.
Frequency response H(f).
Tín hiệu sau khi lọc.
File WAV sau khi lọc.
So sánh phổ trước và sau filtering.
G. Lượng tử hóa, Resampling và Coding
Quantization

Thực hiện lượng tử hóa:

4-bit
8-bit
16-bit

Tính SNR của từng trường hợp.

Resampling

Thực hiện resampling:

44.1 kHz → 16 kHz
44.1 kHz → 8 kHz

So sánh:

Spectrum.
Nyquist frequency.
Chất lượng âm thanh khi nghe.
Coding

Tính:

Theoretical PCM bitrate.
Theoretical PCM file size.
Kích thước file MP3.
Compression ratio.

Công thức PCM bitrate:

R_PCM = Fs × Channels × BitsPerSample

Công thức compression ratio:

Compression Ratio =
Uncompressed Size / Compressed Size
File âm thanh sử dụng

File âm thanh đầu vào của bài thực hành là:

Thien_ly_oi.mp3

File được chuyển sang:

input.wav

ở dạng PCM 16-bit để phục vụ các bước xử lý tiếp theo.

Lưu ý: chuyển MP3 sang WAV không khôi phục lại thông tin đã mất do quá trình nén MP3. WAV chỉ là định dạng lưu trữ PCM cho quá trình xử lý.

Cài đặt thư viện

Cài đặt các thư viện cần thiết:

pip install numpy scipy matplotlib pandas soundfile pydub

Để đọc/chuyển đổi MP3, máy cần có FFmpeg.

Cách chạy
Clone repository:
git clone https://github.com/huylee333/lab01_2351260658_LetrongHuy.git
Di chuyển vào thư mục:
cd lab01_2351260658_LetrongHuy
Mở Notebook:
jupyter notebook Lab01_2351260658.ipynb

hoặc mở trực tiếp bằng VS Code.

Chạy Notebook từ đầu đến cuối theo thứ tự:
01. MP3 → WAV
A → B → C → D → E → F → G
Kết quả đầu ra

Notebook tạo ra các kết quả chính:

Waveform.
FFT spectrum.
Spectrogram.
FIR frequency response.
Audio sau filtering.
Audio sau quantization.
Audio sau resampling.
Bảng SNR.
PCM bitrate.
PCM file size.
Compression ratio.
