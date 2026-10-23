# SAQR TEAM — starter website

واجهة RTL عربية بتصميم أسود ونيون أصفر، متجاوبة للموبايل والكمبيوتر. تشمل شاشة الدخول، ملف العضو، شات، XP/Levels، ترتيب الأعضاء، تاسكات، ولوحة إدارة مبدئية.

## ملفات المشروع
- `index.html`: الواجهة
- `style.css`: التصميم والحركات
- `app.js`: منطق الواجهة
- `config.js`: إعدادات Supabase العامة فقط
- `supabase_schema.sql`: الجداول والصلاحيات ودوال قاعدة البيانات

## تشغيل محلي/نشر Vercel
1. أنشئ مشروع Supabase بالخطة المجانية.
2. افتح SQL Editor وشغّل كامل ملف `supabase_schema.sql`.
3. من Supabase Project Settings > API انسخ Project URL وpublishable/anon key إلى `config.js`.
4. في Authentication > Providers فعّل Discord، وأضف رابط Vercel ضمن Redirect URLs. اضبط Discord OAuth Client ID/Secret في إعدادات المزود حسب تعليمات Supabase.
5. ارفع الملفات إلى جذر مستودع GitHub، ثم استورد المستودع من Vercel. Framework: Other، Build command فارغ، Output directory `.`.
6. بعد أول تسجيل دخول موثوق، خذ UUID من Authentication/Users ثم نفّذ في SQL Editor: `update public.profiles set rank='SAQR' where id='UUID';`
7. من Supabase Database > Replication فعّل Realtime لجدول `chat_messages`.

## أمان مهم
- لا تضع Supabase `service_role` key أو Discord bot token في `config.js` أو GitHub.
- لا تضع كلمة مرور إدارية ثابتة في الواجهة. صلاحيات الإدارة تُتحقق في قاعدة البيانات.
- أقسام التيم الظاهرة هي ADMIN/MOD/EDITOR؛ الرتبة النهائية تُدار من لوحة الإدارة. اختيار رتبة التسجيل طلب فقط.
- حظر الحساب في هذه النسخة يمنع استخدام بيانات الموقع بعد تسجيل الدخول، لكنه لا يمنع OAuth من إنشاء جلسة بالكامل. منع الدخول من أصل المصادقة يتطلب Auth Hook/Edge Function أو backend إضافي.
- رقم الحساب الخاص لا يجب عرضه في قائمة الأعضاء. النسخة الأولية تحفظه لكن لا تعرضه، وإظهار هذا الرقم للإدارة فقط يحتاج Edge Function محمية. اختبر صلاحيات الأعمدة قبل استخدام بيانات حقيقية.
- التحقق من رتب Discord الحقيقية وتغيير رتب Discord يتطلب تكامل بوت/خلفية، مؤجل حسب الاتفاق.
- واجهة طلب اعتماد التاسك معروضة، لكن اعتماد المكافأة الآمن يجب أن يكون من لوحة الإدارة؛ لا تمنح XP بناءً على ضغط العضو وحده.
- عند عدم إعداد `config.js` يعمل `EXPLORE PREVIEW` ببيانات وهمية فقط؛ تسجيل الدخول والشات الحقيقيان غير مفعّلين.
