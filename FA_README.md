# ژئواینتل

![PyPI - Version](https://img.shields.io/pypi/v/geointel?style=flat)


ابزار پایتون با استفاده از API Gemini گوگل برای کشف مکانی که در آن عکس ها از طریق تجزیه و تحلیل موقعیت جغرافیایی هوش مصنوعی گرفته شده است.
## نصب و راه اندازی

```bash
# Basic installation
pip install geointel
```

## نحوه استفاده

### رابط وب (جدید!)

راه اندازی رابط وب تعاملی با یک رابط کاربری مدرن:

```bash
- Standard:
$ geointel --web

- Custom host and port:
$ geointel --web --host 0.0.0.0 --port 4000 
```

<img src="screenshot.jpg" alt="GeoIntel Web Interface">

سپس مرورگر خود را با `http://127.0.0.1:5000`باز کنید.

ویژگی‌ها:
- بارگذاری تصویر کشیدن و رها کردن
- پیکره‌بندی کلید API در مرورگر
- تعاملی 3D گوگل نقشه
- تجزیه و تحلیل هوش مصنوعی در زمان واقعی با توضیحات دقیق

### رابط خط فرمان

```bash
geointel --image path/to/your/image.jpg
```

[![asciicast](https://asciinema.org/a/I6NqhIr6QkBWaaHNjSlieId5s.svg)](https://asciinema.org/a/I6NqhIr6QkBWaaHNjSlieId5s)

Available Arguments

استدلال‌های موجود

توضیحات استدلال
```
--web	Launch web interface (no --image required)
--host	Host address for web interface (default: 127.0.0.1)
--port	Port number for web interface (default: 5000)
--image	Required for CLI mode. Path to the image file or URL to analyze
--context	Additional context information about the image
--guess	Your guess of where the image might have been taken
--output	Output file path to save the results (JSON format)
--api-key	Custom Gemini API key
```

مثال‌ها
```bash
Launch web interface:
$ geointel --web

Basic CLI usage:
$ geointel --image vacation_photo.jpg

With additional context:
$ geointel --image vacation_photo.jpg --context "Taken during summer vacation in 2023"

With location guess:
$ geointel --image vacation_photo.jpg --guess "Mediterranean coast"

Saving results to a file:
$ geointel --image vacation_photo.jpg --output results.json

Using a custom API key:
$ geointel --image vacation_photo.jpg --api-key "your-api-key-here"
```

راه اندازی کلید API

GeoIntel از API Gemini Google استفاده می کند. شما می‌توانید:

```
- Set the API key as an environment variable: GEMINI_API_KEY=your_key_here

- Use the --api-key parameter in the command line
```


کلید Gemini API خود را از Google AI Studio دریافت کنید.

### SDK
```
from geointel import GeoIntel

# Initialize GeoIntel
geointel = GeoIntel()

# Analyze an image and get JSON result
result = geointel.locate(image_path="image.jpg")

# Work with the JSON data
if "error" in result:
    print(f"Error: {result['error']}")
else:
    # Access the first location
    if "locations" in result and result["locations"]:
        location = result["locations"][0]
        print(f"Location: {location['city']}, {location['country']}")
        
        # Get Google Maps URL
        if "coordinates" in location:
            lat = location["coordinates"]["latitude"]
            lng = location["coordinates"]["longitude"]
            maps_url = f"https://www.google.com/maps?q={lat},{lng}"
```

امکانات

   - موقعیت جغرافیایی AI از تصاویر با استفاده از API Gemini گوگل
   - ایجاد لینک های Google Maps بر اساس مختصات تصویر
   - ارائه سطح اطمینان برای پیش بینی مکان
   - پشتیبانی از زمینه های اضافی و حدس های مکان
   - نتایج صادرات به JSON
    - هر دو فایل تصویر محلی و URL های تصویر را اداره می کند

فرمت پاسخ
API یک پاسخ JSON ساختار یافته را با موارد زیر باز می گرداند:

   - تفسیر: تجزیه و تحلیل جامع تصویر
    مکان ها: آرایه ای از مکان های ممکن با:
   - اطلاعات کشور، ایالتی و شهرستان
-    سطح اعتماد به نفس (بالا / متوسط / پایین)
  -  مختصات (عرضه / طول جغرافیایی)
 -   توضیحات مفصلی از استدلال


سلب مسئولیت:

ژئواینتل فقط برای اهداف آموزشی و تحقیقاتی در نظر گرفته شده است. در حالی که از مدل های هوش مصنوعی برای تخمین مکان جایی که یک تصویر گرفته شده است استفاده می کند، پیش بینی های آن دقیق نیست. از این ابزار برای نظارت، تعقیب، اجرای قانون یا هر فعالیتی که ممکن است حریم خصوصی شخصی را نقض کند، قوانین را نقض کند یا باعث آسیب شود، استفاده نکنید.

نویسنده (ها) و مشارکت کنندگان مسئول هیچ گونه خسارت، مسائل حقوقی یا عواقب ناشی از استفاده یا سوء استفاده از این نرم افزار نیستند. از ریسک و اختیار خود استفاده کنید.

همیشه هنگام استفاده از ابزارهای مبتنی بر هوش مصنوعی با قوانین و مقررات محلی، ملی و بین المللی مطابقت داشته باشید.

مشارکت کننده



1. مخزن را فورک کنید

2. ایجاد یک شاخه جدید (گیت پرداخت -b ویژگی / ویژگی جدید).

3. تغییرات خود را متعهد کنید (git commit -am "اضافه کردن ویژگی جدید").

4. فشار به شاخه (گیت فشار ویژگی مبدا / ویژگی جدید).

5. یک درخواست کشش ایجاد کنید.

مجوز

این پروژه تحت مجوز MIT مجوز دارد - برای جزئیات بیشتر به فایل LICENSE مراجعه کنید.
![Star History Chart](https://api.star-history.com/svg?repos=atiilla/geointel&type=Date)
