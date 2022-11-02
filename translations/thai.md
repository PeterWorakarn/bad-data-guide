# The Quartz guide to bad data

**แหล่งอ้างอิงสำหรับปัญหาที่คุณต้องเจอในการทำข้อมูลในโลกแห่งความเป็นจริง
พร้อมแนวทางการแก้ปัญหา**

โลกนี้เต็มไปด้วยชุดข้อมูลที่น่าสนใจมากมาย
แต่ชุดข้อมูลบางอันก็มีปัญหาไม่พร้อมที่ใช้งาน
ตัวบทความนี้จึงตั้งใจที่จะนำเสนอปัญหาเหล่านั้น
พร้อมทั้งแนวทางแก้ไข
เพื่อให้คุณสามารถใช้ประโยชน์จากข้อมูลได้เต็มที่

โดยปัญหาส่วนใหญ่ที่เกิดขึ้นกับชุดข้อมูลสามารถแก้ไขได้
แต่บางอันก็ไม่ใช่ (ซึ่งคุณไม่ควรใช้ชุดข้อมูลนั้น)
หรือบางชุดข้อมูลมีปัญหา แต่ก็ยังสามารถใช้ได้
แต่ต้องใช้ด้วยความระมัดระวัง
เพื่อที่จะทำให้บทความนี้อ่านง่ายขึ้น
บทความนี้จะถูกจัดกลุ่มตามคนที่สามารถแก้ปัญหาได้ดังนี้
ตัวคุณเอง, ที่มาของข้อมูล, ผู้เชี่ยวชาญ และอื่น ๆ
โดยในแต่ละหัวข้อจะมีข้อแนะนำในกรณีคนเหล่านั้นไม่สามารถช่วยแก้ปัญหาให้เราได้

ในบทความนี้ คุณไม่สามารถตรวจสอบทุก ๆ ปัญหา ในทุก ๆ
ชุดข้อมูลของคุณได้ เพราะถ้าทำแบบนั้น
คุณจะไม่ได้เริ่มต้นทำอย่างอื่นเลย แต่อย่างไรก็ตาม
การคุ้นเคยกับปัญหาเหล่านี้
จะช่วยให้งานวิเคราะห์ข้อมูลชิ้นต่อ ๆ ไปของคุณ
มีข้อผิดพลาดน้อย ๆ ลง

ถ้าคุณมีคำถามข้อสงสัยเกี่ยวกับบทความ
โปรดติดต่อมาที่ email
[Chris](mailto:chrisgroskopf@gmail.com).

This work is licensed under a
[Creative Commons Attribution-NonCommercial 4.0 International License](http://creativecommons.org/licenses/by-nc/4.0/).
Send your pull requests!

# คำแปลภาษาอื่น ๆ

- [Chinese](https://web.archive.org/web/20170627153730/http://djchina.org/2016/07/12/bad_data_guide/)
  (complete)
- [Chinese](http://cn.gijn.org/2016/01/10/quartz%E5%9D%8F%E6%95%B0%E6%8D%AE%E6%8C%87%E5%8D%97%E7%B2%BE%E9%80%89%EF%BC%9A%E5%A4%84%E7%90%86%E6%95%B0%E6%8D%AE%E7%9A%84%E6%AD%A3%E7%A1%AE%E6%96%B9%E5%BC%8F%E4%B8%80%E8%A7%88/)
  (partial)
- [Japanese](https://github.com/piyo-ko/bad-data-guide/blob/master/README_ja.md)
- [Portuguese](http://escoladedados.org/2016/09/08/guia-quartz-para-limpeza-de-dados/)
- [Spanish](http://es.schoolofdata.org/guia-quartz/)

ต้องการแปลบทความนี้ในภาษาของคุณ ให้ติดต่อมาที่
Email [Chris](mailto:chrisgroskopf@gmail.com)

# สารบัญ

- [The Quartz guide to bad data](#the-quartz-guide-to-bad-data)
- [คำแปลภาษาอื่น ๆ](#คำแปลภาษาอื่น-ๆ)
- [สารบัญ](#สารบัญ)
  - [หมวดหมู่ปัญหาที่ควรติดต่อเจ้าของแหล่งข้อมูลให้แก้ไข](#หมวดหมู่ปัญหาที่ควรติดต่อเจ้าของแหล่งข้อมูลให้แก้ไข)
  - [หมวดหมู่ปัญหาที่คุณควรให้ผู้เชี่ยวชาญช่วย](#หมวดหมู่ปัญหาที่คุณควรให้ผู้เชี่ยวชาญช่วย)
  - [หมวดหมู่ปัญหาที่คุณควรให้โปรแกรมเมอร์ช่วย](#หมวดหมู่ปัญหาที่คุณควรให้โปรแกรมเมอร์ช่วย)
- [รายละเอียดของแต่ละปัญหา](#รายละเอียดของแต่ละปัญหา)
  - [ปัญหาที่ควรติดต่อเจ้าของแหล่งข้อมูลให้แก้ไข](#ปัญหาที่ควรติดต่อเจ้าของแหล่งข้อมูลให้แก้ไข)
    - [ข้อมูลขาดหายไป](#ข้อมูลขาดหายไป)
    - [ใช้ 0 แทนค่าในส่วนของข้อมูลที่ขาดหายไป](#ใช้-0-แทนค่าในส่วนของข้อมูลที่ขาดหายไป)
    - [ข้อมูลที่ควรจะมีขาดหายไป](#ข้อมูลที่ควรจะมีขาดหายไป)
    - [ข้อมูลมีค่าซ้ำกัน](#ข้อมูลมีค่าซ้ำกัน)
    - [การสะกดศัพท์เฉพาะในข้อมูลไม่เหมือนกันทั้งชุดข้อมูล](#การสะกดศัพท์เฉพาะในข้อมูลไม่เหมือนกันทั้งชุดข้อมูล)
    - [Name order is inconsistent](#name-order-is-inconsistent)
    - [รูปแบบวันที่ไม่เหมือนกันทั้งชุดข้อมูล](#รูปแบบวันที่ไม่เหมือนกันทั้งชุดข้อมูล)
    - [ข้อมูลบางอันไม่ได้ระบุหน่วยที่ชัดเจนเอาไว้](#ข้อมูลบางอันไม่ได้ระบุหน่วยที่ชัดเจนเอาไว้)
    - [Categories are badly chosen](#categories-are-badly-chosen)
    - [หัวข้อของข้อมูล (field name) กำกวม](#หัวข้อของข้อมูล-field-name-กำกวม)
    - [Provenance is not documented](#provenance-is-not-documented)
    - [ระมัดระวังชุดข้อมูลที่น่าสงสัยเหล่านี้เอาไว้](#ระมัดระวังชุดข้อมูลที่น่าสงสัยเหล่านี้เอาไว้)
    - [Data are too coarse](#data-are-too-coarse)
    - [Totals differ from published aggregates](#totals-differ-from-published-aggregates)
    - [Spreadsheet มี 65536 แถว](#spreadsheet-มี-65536-แถว)
    - [Spreadsheet มี 255 คอลั่ม](#spreadsheet-มี-255-คอลั่ม)
    - [Spreadsheet บันทึกข้อมูลวันที่ในปี 1900, 1904, 1969 หรือ 1970](#spreadsheet-บันทึกข้อมูลวันที่ในปี-1900-1904-1969-หรือ-1970)
    - [ข้อความถูกแปลงเป็นตัวเลข](#ข้อความถูกแปลงเป็นตัวเลข)
    - [ตัวเลขถูกเก็บเป็นข้อความ](#ตัวเลขถูกเก็บเป็นข้อความ)
  - [ปัญหาที่คุณควรแก้ด้วยตัวคุณเอง](#ปัญหาที่คุณควรแก้ด้วยตัวคุณเอง)
    - [ข้อมูลเป็นภาษาต่างดาว](#ข้อมูลเป็นภาษาต่างดาว)
    - [Line endings are garbled](#line-endings-are-garbled)
    - [ข้อมูลอยู่ในไฟล์ PDF](#ข้อมูลอยู่ในไฟล์-pdf)
    - [Data are too granular](#data-are-too-granular)
    - [ข้อมูลนั้นถูกบันทึกโดยคน](#ข้อมูลนั้นถูกบันทึกโดยคน)
    - [Data are intermingled with formatting and annotations](#data-are-intermingled-with-formatting-and-annotations)
    - [Aggregations were computed on missing values](#aggregations-were-computed-on-missing-values)
    - [Sample is not random](#sample-is-not-random)
    - [Margin-of-error is too large](#margin-of-error-is-too-large)
    - [Margin-of-error is unknown](#margin-of-error-is-unknown)
    - [Sample is biased](#sample-is-biased)
    - [Data have been manually edited](#data-have-been-manually-edited)
    - [Inflation skews the data](#inflation-skews-the-data)
    - [Natural/seasonal variation skews the data](#naturalseasonal-variation-skews-the-data)
    - [Timeframe has been manipulated](#timeframe-has-been-manipulated)
    - [Frame of reference has been manipulated](#frame-of-reference-has-been-manipulated)
  - [ปัญหาที่คุณควรให้ผู้เชี่ยวชาญช่วย](#ปัญหาที่คุณควรให้ผู้เชี่ยวชาญช่วย)
    - [Author is untrustworthy](#author-is-untrustworthy)
    - [Collection process is opaque](#collection-process-is-opaque)
    - [Data assert unrealistic precision](#data-assert-unrealistic-precision)
    - [There are inexplicable outliers](#there-are-inexplicable-outliers)
    - [An index masks underlying variation](#an-index-masks-underlying-variation)
    - [Results have been p-hacked](#results-have-been-p-hacked)
    - [Benford's Law fails](#benfords-law-fails)
    - [Too good to be true](#too-good-to-be-true)
  - [ปัญหาที่คุณควรให้โปรแกรมเมอร์ช่วย](#ปัญหาที่คุณควรให้โปรแกรมเมอร์ช่วย)
    - [ข้อมูลถูกสรุปรวบยอดมาผิดหมวดหมู่](#ข้อมูลถูกสรุปรวบยอดมาผิดหมวดหมู่)
    - [ข้อมูลถูกจัดเก็บอยู่ในเอกสารที่ถูกสแกน](#ข้อมูลถูกจัดเก็บอยู่ในเอกสารที่ถูกสแกน)

## หมวดหมู่ปัญหาที่ควรติดต่อเจ้าของแหล่งข้อมูลให้แก้ไข

- [Text is garbled](#text-is-garbled)
- [Line endings are garbled](#line-endings-are-garbled)
- [ข้อมูลอยู่ในไฟล์สกุล PDF](#ข้อมูลอยู่ในไฟล์-pdf)
- [Data are too granular](#data-are-too-granular)
- [ข้อมูลนั้นถูกบันทึกโดยคน](#ข้อมูลนั้นถูกบันทึกโดยคน)
- [Data are intermingled with formatting and annotations](#data-are-intermingled-with-formatting-and-annotations)
- [Aggregations were computed on missing values](#aggregations-were-computed-on-missing-values)
- [Sample is not random](#sample-is-not-random)
- [Margin-of-error is too large](#margin-of-error-is-too-large)
- [Margin-of-error is unknown](#margin-of-error-is-unknown)
- [Sample is biased](#sample-is-biased)
- [Data have been manually edited](#data-have-been-manually-edited)
- [Inflation skews the data](#inflation-skews-the-data)
- [Natural/seasonal variation skews the data](#naturalseasonal-variation-skews-the-data)
- [Timeframe has been manipulated](#timeframe-has-been-manipulated)
- [Frame of reference has been manipulated](#frame-of-reference-has-been-manipulated)

## หมวดหมู่ปัญหาที่คุณควรให้ผู้เชี่ยวชาญช่วย

- [Author is untrustworthy](#author-is-untrustworthy)
- [Collection process is opaque](#collection-process-is-opaque)
- [Data assert unrealistic precision](#data-assert-unrealistic-precision)
- [There are inexplicable outliers](#there-are-inexplicable-outliers)
- [An index masks underlying variation](#an-index-masks-underlying-variation)
- [Results have been p-hacked](#results-have-been-p-hacked)
- [Benford's Law fails](#benfords-law-fails)
- [Too good to be true](#too-good-to-be-true)

## หมวดหมู่ปัญหาที่คุณควรให้โปรแกรมเมอร์ช่วย

- [Data are aggregated to the wrong categories or geographies](#data-are-aggregated-to-the-wrong-categories-or-geographies)
- [ข้อมูลถูกจัดเก็บอยู่ในเอกสารที่ถูกสแกน](#ข้อมูลถูกจัดเก็บอยู่ในเอกสารที่ถูกสแกน)

# รายละเอียดของแต่ละปัญหา

## ปัญหาที่ควรติดต่อเจ้าของแหล่งข้อมูลให้แก้ไข

### ข้อมูลขาดหายไป

ระหว่างข้อมูลที่มีค่าว่าง หรือมีค่าเป็น "null"
ในชุดข้อมูลของคุณให้ดีจนกว่าคุณจะมั่นใจว่ามันหมายถึงอะไร
ถ้าข้อมูลนั้นเป็นรายงานประจำปีมันอาจจะหมายถึงว่าข้อมูลที่เป็นค่าว่างนั้นไม่ได้ถูกเก็บข้อมูลไว้หรือป่าว ? หรือถ้าเป็นข้อมูลจากแบบสอบถามอาจแปลได้ว่าผู้ตอบแบบสอบถามเลือกที่จะไม่ตอบคำถามนั้นหรือป่าว ?

ทุก ๆ ครั้งที่คุณต้องทำงานกับข้อมูลที่ขาด ๆ หาย ๆ
ไป คุณควรต้องถามตัวเองว่าคุณเข้าใจจริง ๆ มั้ย ว่าข้อมูลที่หายไปมันหมายถึงอะไร ถ้าคุณไม่ชัวร์หรือไม่แน่ใจว่ามันหมายถึงอะไร คุณควรถามเจ้าของแหล่งข้อมูล

### ใช้ 0 แทนค่าในส่วนของข้อมูลที่ขาดหายไป

ที่แย่ยิ่งกว่าการที่ข้อมูลขาดหายไป คือการใส่ค่าตัวแทนลงไปแทนอย่างเช่น การใส่ค่า `0` ลงไป
ซึ่งนี่อาจจะเป็นผลลัพธ์ของการกระทำโดยไม่ตั้งใจหรือเป็นการทำผ่านการเขียนโปรแกรมที่ไม่รู้วิธีจัดการกับค่าว่างที่เหมาะสม ไม่ว่าในกรณีใดก็ตาม หากคุณเจอเลข `0` ในชุดข้อมูลของคุณ คุณควรถามตัวเองว่าข้อมูลตรงนั้นมีค่าเป็น `0` หรือหมายถึงเป็นค่าว่าง ไม่มีค่า (มีบางกรณีเราจะเจอชุดข้อมูลที่เป็น `-1` ได้เช่นกัน) 

ถ้าคุณไม่ชัวร์หรือไม่แน่ใจว่ามันหมายถึงอะไร คุณควรถามเจ้าของแหล่งข้อมูล

ข้อควรระวังนี้สามารถนำไปใช้ได้กับข้อมูลแบบ non-numerical values ที่ `0` อาจหมายถึงสิ่งอื่น เช่น `0` ในข้อมูลวันที่ จะแสดงผลเป็น `1970-01-01T00:00:00Z` or `1969-12-31T23:59:59Z` ซึ่งเป็น [Unix epoch for timestamps](https://en.wikipedia.org/wiki/Unix_time#Encoding_time_as_a_number)

หรือ

`0` ในข้อมูลภูมิศาสตร์ จะแสดงผลเป็น `0°00'00.0"N+0°00'00.0"E` หรือ เขียนอย่างง่ายแบบนี้ `0°N 0°E` ซึ่งเป็นจุดเล็ก ๆ ในมหาสมุทร แอตแลนติก ที่อยู่ทางใต้ของกาน่า รู้จักกันในชื่อ [Null Island](https://en.wikipedia.org/wiki/Null_Island).

เนื้อหาที่เกี่ยวข้อง:

- [Suspicious values are present](#suspicious-values-are-present)
- [Spreadsheet has dates in 1900, 1904, 1969, or 1970](#spreadsheet-has-dates-in-1900-1904-1969-or-1970)


### ข้อมูลที่ควรจะมีขาดหายไป

บางครั้งข้อมูลหายไปจากชุดข้อมูล และเราไม่สามารถตรวจเช็คได้จากตัวชุดข้อมูลอย่างเดียว แต่เรารู้จากความรู้ ความเข้าใจของเราเองว่าข้อมูลขาดหายไป เช่น ชุดข้อมูลเกี่ยวกับรัฐในสหรัฐอเมริกา ตรงนี้เราก็สามารถตรวจสอบได้ว่าชุดข้อมูลมีรัฐในสหรัฐอเมริกาครบหรือไม่ (และอย่าลืม
[พื้นที่ชายแดน](https://en.wikipedia.org/wiki/Territories_of_the_United_States) 50 รัฐไม่ใช่เลขที่ถูกต้อง ถ้าชุดข้อมูลนั้นรวมรัฐ Puerto Rico.) 

ถ้าคุณกำลังเล่นกับข้อมูลผู้เล่นเบสบอล จงตรวจสอบให้ดีว่ามีทีมครบทุกทีม โดยคุณอาจจะตรวจสอบแบบเร็ว ๆ  และใช้สัญชาตญาณเพื่อดูว่ามีอะไรขาดหายไปมั้ย

### ข้อมูลมีค่าซ้ำกัน

If the same row appears in your dataset more than
once you should find out why. Sometimes it need
not be a whole row. Some campaign finance data
include "amendments" that use the same unique
identifiers as the original transaction. If you
didn't know that then any calculations you did
with the data would be wrong. If something seems
like it should be unique verify that it is. If you
discover that it isn't, ask your source why.

### การสะกดศัพท์เฉพาะในข้อมูลไม่เหมือนกันทั้งชุดข้อมูล

การสะกดคำผิด ๆ ถูก ๆ เป็นสัญญาณที่เห็นได้ชัดเลยว่าข้อมูลนั้นถูกกรอกโดยการใช้คนมานั่งกรอกทีละบรรทัด
และอย่าสังเกตการสะกดผิด ๆ ถูก ๆ แค่ชื่อของคน
(ซึ่งหลาย ๆ ครั้งมันก็ตรวจสอบยากมาก ๆ
ว่าสะกดผิดรึป่าว)
เพราะสิ่งที่เจอบ่อยที่สุดคือชื่อสถานที่เฉพาะ
หรือชื่อถนน ชื่อเมืองต่าง ๆ (`Los Angelos`
เป็นชื่อเฉพาะที่บางทีก็สะกดไม่เหมือนกัน)
และถ้าหากคุณเจอสัญญาณเหล่านี้ที่บอกว่าข้อมูลเหล่านี้ถูกกรอกโดยการใช้คนมานั่งกรอกทีละบรรทัด
ไม่ได้หมายความว่าคุณจะใช้ข้อมูลนั้นไม่ได้เลย
แต่คุณต้องทำใจว่า
คุณอาจจะต้องมานั่งไล่เช็คตรวจสอบอีกที
เพื่อให้ข้อมูลของคุณมีความถูกต้อง

[OpenRefine's](http://openrefine.org/)
เป็นเครื่องมือสำหรับ
[text clustering](https://github.com/OpenRefine/OpenRefine/wiki/Clustering)
จะช่วยคุณทำความสะอาดข้อมูลผ่านการแนะนำคำที่ถูกต้องในบรรดาคำที่สะกดผิดด้วยกัน
(อย่างเช่น, `Los Angelos` และ `Los Angeles`
เป็นคำเดียวกัน เพียงแต่สะกดผิด). แต่อย่างไรก็ตาม
[document the changes you make](https://github.com/OpenRefine/OpenRefine/wiki/Exporters)
เพื่อที่จะมั่นใจใน
[good data provenance](#provenance-is-not-documented).

รายละเอียดเพิ่มเติม:

- [ข้อมูลนั้นถูกบันทึกโดยคน](#ข้อมูลนั้นถูกบันทึกโดยคน)

### Name order is inconsistent

Does your data have Middle Eastern or East Asian
names in it? Are you sure the surnames are always
in the same place? Is it possible anyone in your
dataset
[uses a mononym](https://en.wikipedia.org/wiki/Indonesian_names#Indonesian_naming_system)?
These are the sorts of things that data makers
habitually get wrong. If you're working with a
list of ethnically diverse names—which is any list
of names—then you should do at least a cursory
review before assuming that joining the
`first_name` and `last_name` columns will give you
something that is appropriate to publish.

- [ข้อมูลนั้นถูกบันทึกโดยคน](#ข้อมูลนั้นถูกบันทึกโดยคน)

### รูปแบบวันที่ไม่เหมือนกันทั้งชุดข้อมูล

วันที่ไหนคือวันในเดือนเดือนกันยายน ?

- `10/9/15`
- `9/10/15`

ถ้าข้อแรกถูกบันทึกโดยคนยุโรป
ส่วนข้อที่สองถูกบันทึกโดยคนอเมริกัน
[ข้อมูลสองชุดนี้จะเหมือนกัน](https://en.wikipedia.org/wiki/Date_format_by_country).
การที่เราไม่รู้ที่มาที่ไปของการบันทึกข้อมูล
เราจึงไม่สามารถแน่ใจได้เลยว่าเราแปลความได้ถูกต้อง
ดังนั้นคุณอาจจะต้องลองกลับไปตรวจสอบที่มา
หรือถามเจ้าของข้อมูลอีกทีเพื่อความแน่ใจ

- [ข้อมูลนั้นถูกบันทึกโดยคน](#ข้อมูลนั้นถูกบันทึกโดยคน)
- [Provenance is not documented](#provenance-is-not-documented)

### ข้อมูลบางอันไม่ได้ระบุหน่วยที่ชัดเจนเอาไว้

แม้ว่า `น้ำหนัก` หรือ `ราคา` จะสื่อความหมายว่าเป็น หน่วยของการวัด แต่ก็เพิ่งอย่างด่วยสรุปว่าข้อมูลนั้นถูกบันทึกในประเทศ สหรัฐอเมริกา ที่ใช้หน่วยน้ำหนักเป็น ปอนด์ และคิดราคาเป็น ดอลลาร์ 
ข้อมูลทางวิทยาศาสตร์ส่วนใหญ่มีหน่วยวัดเสมอ และแต่ละประเทศจะมีหน่วยวัดเฉพาะของตัวเอง ถ้าเกิดในชุดข้อมูลไม่ได้ระบุหน่วยวัดที่ชัดเจน คุณควรจะกลับไปเช็คแหล่งที่มาของชุดข้อมูล

แต่ถึงแม้ว่าชุดข้อมูลบอกหน่วยวัดชัดเจน แต่หน่วยวัดส่วนใหญ่แล้วจะเปลี่ยนแปลงตามกาลเวลาเช่น ค่าเงินดอลลาร์ในปี 2010 ไม่ได้มีมูลค่าเท่ากับค่าเงินดอลลาร์ในวันนี้ 

และ [ton](https://en.wikipedia.org/wiki/Short_ton) ไม่เหมือนกับ
[ton](https://en.wikipedia.org/wiki/Long_ton) หรือ [tonne](https://en.wikipedia.org/wiki/Tonne)

เนื้อหาที่เกี่ยวข้อง:

- [Field names are ambiguous](#field-names-are-ambiguous)
- [Inflation skews the data](#inflation-skews-the-data)

### Categories are badly chosen

Watch out for values which purport to be only
`true` or `false`, but really aren't. This is
often the case with surveys where `refused` or
`no answer` are also valid—and meaningful—values.
Another common problem is the usage of any kind of
`other` category. If the categories in a dataset
are a bunch of countries and an `other`, what does
that mean? Does it mean that the person collecting
the data didn't know the right answer? Were they
in international waters? Expatriates? Refugees?

Bad categories can also artificially exclude data.
This frequently happens with crime statistics. The
FBI has defined the crime of "rape" in a variety
of different ways over time. In fact, they've done
such a poor job of figuring out what rape is that
many criminologists argue their statistics should
not be used at all. A bad definition might mean a
crime is counted in a different category than you
expect or that it wasn't counted at all. Be
exceptionally ware of this problem when working
with topics where definitions tend to be
arbitrary, such as `race` or `ethnicity`.

### หัวข้อของข้อมูล (field name) กำกวม

`residence` หรือ `ที่อยู่อาศัย` หมายถึงอะไร ?
หมายถึงที่ ๆ คน ๆ นึงอยู่จริง ๆ หรือที่อยู่ตามทะเบียน

หัวข้อของข้อมูล (Field names) บางทีก็ไม่เจาะจงเหมือนที่เราคิด และส่วนใหญ่สามารถตีความได้มากกว่าหนึ่งอย่าง และถึงแม้ว่าคุณเข้าใจข้อมูลนั้น แต่ก็อาจเป็นไปได้ว่าคนกรอกข้อมูลนั้น จะสับสนและกรอกข้อมูลผิดแทน

### Provenance is not documented

Data are created by a variety of kinds of
individuals and organizations including
businesses, governments, nonprofits and nut-job
conspiracy theorists. Data are gathered in many
different ways including surveys, sensors and
satellites. It may be typed, tapped or scribbled.
Knowing where your data came from can give you a
huge amount of insight into its limitations.

Survey data, for example, is rarely exhaustive.
Sensors vary in their accuracy. Governments are
often disinclined to give you unbiased
information. Data from a war zone may have a
strong geographical bias due to the danger of
crossing battle lines. To make this situation
worse, these different sources are often
daisy-chained together. Policy analysts frequently
redistribute data they got from the government.
Data that were written by a doctor may be keyed by
a nurse. Every stage in that chain is an
opportunity for error. Know where your data came
from.

เนื้อหาที่เกี่ยวข้อง:

- [Units are not specified](#units-are-not-specified)

### ระมัดระวังชุดข้อมูลที่น่าสงสัยเหล่านี้เอาไว้

ถ้าคุณเห็นข้อมูลเหล่านี้ในชุดข้อมูล ให้จัดการข้อมูลนั้นด้วยความระมัดระวัง:

ข้อมูลที่เป็นตัวเลข:

- [`65,535`](https://en.wikipedia.org/wiki/65535_%28number%29)
- [`255`](https://en.wikipedia.org/wiki/255_%28number%29)
- [`2,147,483,647`](https://en.wikipedia.org/wiki/2147483647_%28number%29)
- [`4,294,967,295`](https://en.wikipedia.org/wiki/4294967295)
- [`555-3485`](https://en.wikipedia.org/wiki/555_%28telephone_number%29)
- `99999` (หรือ อะไรที่มีเลข 9 ยาวมาก ๆ)
- `00000` (หรือ อะไรที่มีเลข 0 ยาวมาก ๆ)

ข้อมูลที่เป็นวัน เวลา:

- [`1970-01-01T00:00:00Z`](https://en.wikipedia.org/wiki/Unix_time#Encoding_time_as_a_number)
- [`1969-12-31T23:59:59Z`](https://en.wikipedia.org/wiki/Unix_time#Encoding_time_as_a_number)
- [`January 1st, 1900`](#spreadsheet-has-dates-in-1900-1904-1969-or-1970)
- [`January 1st, 1904`](#spreadsheet-has-dates-in-1900-1904-1969-or-1970)

ข้อมูลเชิงภูมิศาสตร์:

- [`0°00'00.0"N+0°00'00.0"E`](https://en.wikipedia.org/wiki/Null_Island)
  หรือ เขียนอย่างย่อว่า
  [`0°N 0°E`](https://en.wikipedia.org/wiki/Null_Island)
- US zip code `12345` (Schenectady, New York)
- US zip code `90210` (Beverly Hills, CA)

ข้อมูลแต่ละอันที่กล่าวถึง อาจจะบ่งบอกได้ถึงข้อผิดพลาดที่เกิดโดยคน หรือโดยคอมพิวเตอร์ ถ้าคุณเจอข้อมูลในลักษณะให้ตรวจสอบให้แน่ใจอีกทีว่ามันหมายถึงสิ่งที่คุณคิดจริงหรือไม่ ?

เนื้อหาที่เกี่ยวข้อง:

- [Spreadsheet has 65536 rows](#spreadsheet-has-65536-rows)
- [Spreadsheet has 255 columns](#spreadsheet-has-255-columns)
- [Spreadsheet has dates in 1900 or 1904](#spreadsheet-has-dates-in-1900-or-1904)

### Data are too coarse

You've got states and you need counties. You've
got employers and you need employees. They gave
you years, but you want months. In many cases we
get data that have been aggregated too much for
our purposes.

Data usually cannot be disaggregated once they
have been merged together. If you're given data
that are too coarse, you'll need to ask your
source for something more specific. They may not
have it. If they do have it they may not be able
or willing to give it to you. There are many
federal datasets that can't be accessed at the
local level to protect the privacy of individuals
who might be uniquely identified by them. (For
example, a single Somali national living in
western Texas.) All you can do is ask.

One thing you should never ever do is divide a
yearly value by 12 and call it the "average per
month". Without knowing the distribution of the
values, that number will be meaningless. (Maybe
all instances occurred in one month or one season.
Maybe the data follows an exponential trend
instead of a linear one.) It's wrong. Don't do it.

เนื้อหาที่เกี่ยวข้อง:

- [Data are too granular](#data-are-too-granular)
- [Data are aggregated to the wrong categories or geographies](#data-are-aggregated-to-the-wrong-categories-or-geographies)

### Totals differ from published aggregates

Imagine that after a long FOIA fight you receive a
"complete" list of incidents of police
use-of-force. You open it up and discover it has
2,467 rows. Great, time to report it out. Not so
fast. Before you publish anything from that
dataset go find the last time that police chief
went on the record about his department's use of
force. You may find that in an interview six weeks
earlier he said "less than 2,000 times" or that he
named a specific number and it doesn't match your
dataset.

These sorts of discrepancies between published
statistics and raw data can be a very great source
of leads. Often the answer will be simple. For
instance, the data you were given may not cover
the same time period he was speaking about. But
sometimes you'll catch them in a lie. Either way,
you should make sure the published numbers match
the totals for the data you're given.

### Spreadsheet มี 65536 แถว

ในโปรแกรม Excel รุ่นเก่าสามารถบันทึกข้อมูลได้มากสุด 65,536 แถว ถ้าคุณได้รับชุดข้อมูลที่มีข้อมูลเท่ากับ 65,536 แถว เป็นไปได้ได้ว่าชุดข้อมูลจะถูกตัดทิ้งออกให้สามารถบันทึกในโปรแกรม Excel ได้ ดังนั้นคุณควรสอบถามเจ้าของข้อมูลถึงชุดข้อมูลที่เหลือ

สำหรับโปรแกรม Excel รุ่นใหม่สามารถบันทึกข้อมูลได้มากสุด 1,048,576 แถว ซึ่งมันเป็นไปได้น้อย ๆ มาก ที่คุณจะต้องทำงานกับชุดข้อมูลที่มีข้อมูลขนาดนั้น (ในชุดข้อมูลที่ใหญ่ขนาดนั้นจะถูกใช้ผ่านโปรแกรมอื่นแทน)

### Spreadsheet มี 255 คอลั่ม

[โปรแกรม Numbers ใน Apple](https://www.apple.com/numbers/) สามารถจัดการ spreadsheets ได้แค่ 255 คอลั่ม และเมื่อเกินกว่านั้น ตัวโปรแกรมจะทิ้งข้อมูลที่เกินกว่านั้นโดยไม่แจ้งเตือนผู้ใช้แต่อย่างเดียว

ถ้าเกิดคุณได้รับชุดข้อมูลที่ข้อมูลแค่ 255 คอลั่ม ให้ลองตรวจสอบดูว่าไฟล์นั้นถูกเปิด หรือเซฟข้อมูลด้วยโปรแกรม Numbers หรือไม่ ?

### Spreadsheet บันทึกข้อมูลวันที่ในปี 1900, 1904, 1969 หรือ 1970

For reasons beyond obscure, Excel's default date
from which it counts all other dates is
`January 1st, 1900`, _unless_ you're using Excel
on a Mac, in which case it's `January 1st, 1904`.
There are a variety of ways in which data in Excel
can be entered or calculated incorrectly and end
up as one of these two dates. If you spot them in
your data, it's probably an issue.

Many databases and applications will often
generate a date of `1970-01-01T00:00:00Z` or
`1969-12-31T23:59:59Z` which is the
[Unix epoch for timestamps](https://en.wikipedia.org/wiki/Unix_time#Encoding_time_as_a_number).
In other words this is what happens when a system
tries to display an empty value or a `0` value as
a date.

### ข้อความถูกแปลงเป็นตัวเลข

ไม่ใช่จำนวนนับทุกอันถูกเก็บเป็นตัวเลข อย่างเช่น สำนักงานสํารวจสํามะโนประชากรของประเทศสหรัฐอเมริกาใช้ "รหัส FIPS" ในการระบุสถานที่ในประเทศ และรหัสพวกคือตัวเลขยาว ๆ ซึ่งมันไม่ใช่จำนวนนับ
`037` ในรหัส FIPS หมายถึง เมือง Los Angeles ซึ่งมันไม่เหมือนตัวเลข (จำนวนนับ) `37` 


 Not all numerals are numbers. For instance, the US
Census Bureau uses "FIPS codes" to identify every
place in the United States. These codes are of
various lengths and are numeric. However, they are
_not_ numbers. `037` is the FIPS code for Los
Angeles County. It is not the number `37`. The
numerals `37` are, however, a valid FIPS code: for
North Carolina. Excel and other spreadsheets will
often make the mistake of assuming numerals are
numbers and stripping the leading zeros. This can
cause all kinds of problems if you try to convert
it to another file format or merge it with another
dataset. Watch out for data where this has
happened before it was given to you.

### ตัวเลขถูกเก็บเป็นข้อความ

When working with spreadsheets, numbers may be
stored as text with unwanted formatting. This
often happens when a spreadsheet is optimized for
presenting data rather than making it available
for re-use. For example, instead of representing a
million dollars with the number "1000000" a cell
might contain the string "1,000,000" or "1 000
000" or "USD 1,000,000" with the formatting of
commas, units and spaces entered as characters.
Excel can take care of some simple cases with
built-in functions, but you'll often need to use
formulas to strip out characters until cells are
clean enough to be recognized as numbers. Good
practice is to store numbers without formatting
and to include supporting information in column
names or metadata.

## ปัญหาที่คุณควรแก้ด้วยตัวคุณเอง

### ข้อมูลเป็นภาษาต่างดาว

All letters are represented by computers as
numbers. Encoding problems are issues that arise
when text is represented by a specific set of
numbers (called an "encoding") and you don't know
what it is. This leads to a phenomenon called
[mojibake](https://en.wikipedia.org/wiki/Mojibake)
where the text in your data looks like garbage, or
like this: ���.

In the vast majority of cases your text editor or
spreadsheet application will figure out the
correct encoding, however, if it screws it up you
could be publishing somebody's name with a weird
character in the middle. Your source should be
able to tell you what encoding your data are in.
In the event they can't there are ways of guessing
that are about fairly reliable. Ask a programmer.

### Line endings are garbled

All text and "text data" files, such as CSV, use
invisible characters to represent the ends of
lines. Windows, Mac and Linux computers have
historically disagreed about what these line
ending characters should be. Attempting to open a
file saved on one operating system from another
operating system can sometimes cause Excel or
other applications to fail to properly identify
the line breaks.

Typically, this is easy to resolve by simply
opening the file in any general-purpose text
editor and re-saving it. If the file is
exceptionally large you may need to consider using
a command-line tool or enlisting the help of a
programmer. You can read more about this issue
[here](https://nicercode.github.io/blog/2013-04-30-excel-and-line-endings/).

### ข้อมูลอยู่ในไฟล์ PDF

ข้อมูลส่วนใหญ่ โดยเฉพาะข้อมูลเปิดจากรัฐบาล ส่วนใหญ่จะถูกจัดเก็บอยู่ในไฟล์สกุล PDF ถ้าเกิดคุณต้องการข้อมูลจากไฟล์นั้นจริง ๆ คุณสามารถเลือกที่จะดึงข้อมูลออกมาได้ (ถ้าคุณได้
[เอกสารที่ถูกสแกน](#ข้อมูลถูกจัดเก็บอยู่ในเอกสารที่ถูกสแกน)
ซึ่งเป็นอีกปัญหานึง) หนึ่งในเครื่องมือฟรีที่ดีตัวนึงคือ [Tabula](http://tabula.technology/)

แต่ถ้าคุณมี Adobe Creative Cloud และมี Acrobat Pro คุณจะสามารถใช้ฟีเจอร์ในการดึงข้อมูลออกมาจากไฟล์สกุล PDF เป็นไฟล์สกุล Excel ได้ ไม่ว่าแนวทางไหนก็ควรจะสามารถดึงข้อมูลออกมาจากไฟล์สกุล PDF ได้

เนื้อหาที่เกี่ยวข้อง:

- [ข้อมูลถูกจัดเก็บอยู่ในเอกสารที่ถูกสแกน](#ข้อมูลถูกจัดเก็บอยู่ในเอกสารที่ถูกสแกน)

### Data are too granular

This is the opposite of
[Data are too coarse](#data-are-too-coarse). In
this case you've got counties, but you want states
or you've got months but you want years.
Fortunately this is usually pretty
straightforward.

Data can be aggregated by using the Pivot Table
feature of Excel or Google Docs, by using a SQL
database or by writing custom code. Pivot Tables
are a fabulous tool that every reporter should
learn, but they do have their limits. For
exceptionally large datasets or aggregations to
unusual groups you should ask a programmer and
they can craft a solution that's easier to verify
and reuse.

เนื้อหาที่เกี่ยวข้อง:

- [Data are too coarse](#data-are-too-coarse)
- [Data are aggregated to the wrong categories or geographies](#data-are-aggregated-to-the-wrong-categories-or-geographies).

### ข้อมูลนั้นถูกบันทึกโดยคน

Human data entry is such a common problem that
symptoms of it are mentioned in at least 10 of the
other issues described here. There is no worse way
to screw up data than to let a single human type
it in, without validation. For example, I once
acquired the complete dog licensing database for
Cook County, Illinois. Instead of requiring the
person registering their dog to choose a breed
from a list, the creators of the system had simply
given them a text field to type into. As a result
this database contained at least 250 spellings of
`Chihuahua`. Even with the best tools available,
data this messy can't be saved. They are
effectively meaningless. This is not that
important with dog data, but you don't want it
happening with wounded soldiers or stock tickers.
Beware human-entered data.

### Data are intermingled with formatting and annotations

Complex representations of data such as HTML and
XML allow for a clean separation between data and
formatting, but this is not the case for common
tabular representations of data such as a
spreadsheet. Yet, people still try. A common
problem with data provided as a spreadsheet is
that the first few rows of data will actually be
descriptions or notes about the data rather than
column headings or data itself. A key or data
dictionary may also be placed in the middle of the
spreadsheet. Header rows may be repeated. Or the
spreadsheet will include multiple tables (which
may have different column headings) one after the
other in the same sheet rather than separated into
different sheets.

In all of these cases the main solution is simply
to identify the problem. Obviously trying to
perform any analysis on a spreadsheet that has
these kinds of problems will fail, sometimes for
non-obvious reasons. When looking at new data for
the first time it's always a good idea to ensure
there aren't extra header rows or other formatting
characters inserted amongst the data.

### Aggregations were computed on missing values

Imagine a dataset with 100 rows and a column
called `cost`. In 50 of the rows the `cost` column
is blank. What is the average of that column? Is
it `sum_of_cost / 50` or `sum_of_cost / 100`?
There is no one definitive answer. In general, if
you're going to compute aggregates on columns that
are missing data, you can safely do so by
filtering out the missing rows first, but be
careful not to compare aggregates from two
different columns where different rows were
missing values! In some cases the missing values
might also be legitimately interpreted as `0`. If
you're not sure, ask an expert or just don't do
it.

This is an error you can make in your analysis,
but it's also an error that others can make and
pass on to you, so watch out for it if data comes
to you with aggregates already computed.

เนื้อหาที่เกี่ยวข้อง:

- [Values are missing](#values-are-missing)
- [Zeros replace missing values](#zeros-replace-missing-values)

### Sample is not random

A non-random sampling error occurs when a survey
or other sampled dataset either intentionally or
accidentally fails to cover the entire population.
This can happen for a variety of reasons ranging
from time-of-day to the respondent's native
language and is a common source of error in
sociological research. It can also happen for less
obvious reasons, such as when a researcher thinks
they have a complete dataset and chooses to work
with only part of it. If the original dataset was
incomplete for any reason then any conclusions
drawn from their sample will be incorrect. The
only thing you can do to fix a non-random sample
is avoid using that data.

เนื้อหาที่เกี่ยวข้อง:

- [Sample is biased](#sample-is-biased)

### Margin-of-error is too large

I know of no other single issue that causes more
reporting errors than the unreflective usage of
numbers with very large margins-of-error. MOE is
usually associated with survey data. The most
likely place a reporter encounters it is when
using polling data or the US Census Bureau's
[American Community Survey](https://www.census.gov/programs-surveys/acs/)
data. The MOE is a measure of the range of
possible true values. It may be expressed as a
number (`400 +/- 80`) or as a percentage of the
whole (`400 +/- 20%`). The smaller the relevant
population, the larger the MOE will be. For
example, according to the 2014 5-year ACS
estimates, the number of Asians living in New York
is `1,106,989 +/- 3,526` (0.3%). The number of
Filipinos is `71,969 +/- 3,088` (4.3%). The number
of Samoans is `203 +/- 144` (71%).

The first two numbers are safe to report. The
third number should never be used in published
reporting. There is no one rule about when a
number is not accurate enough to use, but as a
rule of thumb, you should be cautious about using
any number with a MOE over 10%.

เนื้อหาที่เกี่ยวข้อง:

- [Margin-of-error is unknown](#margin-of-error-is-unknown)

### Margin-of-error is unknown

Sometimes the problem isn't that the margin of
error is
[too large](#margin-of-error-is-too-large), it's
that nobody ever bothered to figure out what it
was in the first place. This is one problem with
unscientific polls. Without computing a MOE, it is
impossible to know how accurate the results are.
As a general rule, anytime you have data that are
from a survey you should ask for what the MOE is.
If the source can't tell you, those data probably
aren't worth using for any serious analysis.

เนื้อหาที่เกี่ยวข้อง:

- [Margin-of-error is too large](#margin-of-error-is-too-large)

### Sample is biased

Like
[a sample that is not random](#sample-is-not-random),
a biased sample results from a lack of care with
how the sampling is executed. Or, from willfully
misrepresenting it. A sample might be biased
because it was conducted on the internet and
poorer people don't use the internet as frequently
as the rich. Surveys must be carefully weighted to
ensure they cover proportional segments of any
population that could skew the results. It's
almost impossible to do this perfectly so it is
often done wrong.

เนื้อหาที่เกี่ยวข้อง:

- [Sample is not random](#sample-is-not-random)

### Data have been manually edited

Manual editing is almost the same problem as
[data being entered by humans](#ข้อมูลนั้นถูกบันทึกโดยคน)
except that it happens after the fact. In fact,
data are often manually edited in an attempt to
fix data that were originally entered by humans.
Problems start to creep in when the person doing
the editing doesn't have complete knowledge of the
original data. I once saw someone spontaneously
"correct" a name in a dataset from `Smit` to
`Smith`. Was that person's name really `Smith`? I
don't know, but I do know that value is now a
problem. Without a record of that change, it's
impossible to verify what it should be.

Issues with manual editing are one reason why you
always want to ensure your data have
[well-documented provenance](#provenance-is-not-documented).
A lack of provenance can be a good indication that
someone may have monkeyed with it. Academics and
policy analysts often get data from the
government, monkey with them and then redistribute
them to journalists. Without any record of their
changes it's impossible to know if the changes
they made were justified. Whenever feasible always
try to get the _primary source_ or at least the
earliest version you can and then do your own
analysis from that.

เนื้อหาที่เกี่ยวข้อง:

- [Provenance is not documented](#provenance-is-not-documented)
- [ข้อมูลนั้นถูกบันทึกโดยคน](#ข้อมูลนั้นถูกบันทึกโดยคน)

### Inflation skews the data

Currency inflation means that over time money
changes in value. There is no way to tell if
numbers have been "inflation adjusted" just by
looking at them. If you get data and you aren't
sure if they have been adjusted then check with
your source. If they haven't you'll likely want to
perform the adjustment. This
[inflation adjuster](http://inflation-adjust.herokuapp.com/)
is a good place to start.

เนื้อหาที่เกี่ยวข้อง:

- [Natural/seasonal variation skews the data](#nationalseasonal-variation-skews-the-data)

### Natural/seasonal variation skews the data

Many types of data fluctuate naturally due to some
underlying forces. The best known example of this
is employment fluctuating with the seasons.
Economists have developed a variety of methods of
compensating for this variation. The details of
those methods aren't particularly important, but
it is important that you know if the data you're
using have been "seasonally adjusted". If they
haven't and you want to compare employment from
month to month you will probably want to get
adjusted data from your source. (Adjusting them
yourself is much harder than with inflation.)

เนื้อหาที่เกี่ยวข้อง:

- [Inflation skews the data](#inflation-skews-the-data)

### Timeframe has been manipulated

A source can accidentally or intentionally
misrepresent the world by giving you data that
stops or starts at a specific time. For a potent
example see 2015's widely reported "national crime
wave". There was no crime wave. What there was was
a series of spikes in particular cities when
compared to just the last few years. Had
journalists examined a wider timeframe they would
have seen that violent crime was higher virtually
everywhere in the US ten years before. And twenty
years before it was nearly double.

If you have data that covers a limited timeframe
try to avoid starting your calculations with the
very first time period you have data for. If you
start a few years (or months or days) into the
data you can have confidence that you aren't
making a comparison which would be invalidated by
having a single additional data point.

เนื้อหาที่เกี่ยวข้อง:

- [Frame of reference has been manipulated](#frame-of-reference-has-been-manipulated)

### Frame of reference has been manipulated

Crime statistics are often manipulated for
political purposes by comparing to a year when
crime was very high. This can be expressed either
as a change (down `60%` since 2004) or via an
index (`40`, where 2004 = 100). In either of these
cases, 2004 may or may not be an appropriate year
for comparison. It could have been an unusually
high crime year.

This also happens when comparing places. If I want
to make one country look bad, I simply express the
data about it relative to whichever country is
doing the best.

This problem tends to crop up in subjects where
people have a strong confirmation bias. ("Just as
I thought, crime is up!") Whenever possible try
comparing rates from several different starting
points to see how the numbers shift. And whatever
you do, _don't use this technique yourself_ to
make a point you think is important. That's
inexcusable.

เนื้อหาที่เกี่ยวข้อง:

- [Timeframe has been manipulated](#timeframe-has-been-manipulated)

## ปัญหาที่คุณควรให้ผู้เชี่ยวชาญช่วย

### Author is untrustworthy

Sometimes the only data you have are from a source
you would rather not rely on. In some situations
that's just fine. The only people who know how
many guns are made are gun manufacturers. However,
if you have data from a questionable maker always
check it with another expert. Better yet, check it
with two or three. Don't publish data from a
biased source unless you have substantial
corroborating evidence.

### Collection process is opaque

It's very easy for false assumptions, errors or
outright falsehoods to be introduced into these
data collection processes. For this reason it's
important that methods used be transparent. It's
rare that you'll know exactly how a dataset was
gathered, but indications of a problem can include
numbers that
[assert unrealistic precision](#data-asserts-unrealistic-precision)
and data that
[are too good to be true](#too-good-to-be-true).

Sometimes the origin story may just be fishy: did
such-and-such academic really interview 50 active
gang members from the south side of Chicago? If
the way the data were gathered seems questionable
and your source can't offer you
[ironclad provenance](#provenance-is-not-documented)
then you should always verify with another expert
that the data could reasonably have been collected
in the way that was described.

เนื้อหาที่เกี่ยวข้อง:

- [Provenance is not documented](#provenance-is-not-documented)
- [Data assert unrealistic precision](#data-assert-unrealistic-precision)
- [Too good to be true](#too-good-to-be-true)

### Data assert unrealistic precision

Outside of hard science, few things are routinely
measured with more than two decimal places of
accuracy. If a dataset lands on your desk that
purports to show a factory's emissions to the 7th
decimal place that is a dead giveaway that it was
estimated from other values. That in and of itself
may not be a problem, but it's important to be
transparent about estimates. They are often wrong.

### There are inexplicable outliers

I recently created a dataset of how long it takes
for messages to reach different destinations over
the internet. All of the times were in the range
from `0.05` to `0.8` seconds, except for three.
The other three were all over `5,000` seconds.
This is a major red flag that something has gone
wrong in the production of the data. In this
particular case an error in the code I wrote
caused some failures to continue counting while
all other messages were being sent and received.

Outliers such as these can dramatically screw up
your statistics—especially if you're using
averages. (You should probably be using medians.)
Whenever you have a new dataset it is a good idea
to take a look at the largest and smallest values
and ensure they are in a reasonable range. If the
data justifies it you may also want to do a more
statistically rigorous analysis using
[standard deviations](https://en.wikipedia.org/wiki/Standard_deviation)
or
[median deviations](https://en.wikipedia.org/wiki/Median_absolute_deviation).

As a side-benefit of doing this work, outliers are
often a great way to find story leads. If there
really was one country where it took 5,000 times
as long to send a message over the internet, that
would be a great story.

### An index masks underlying variation

Analysts who want to follow the trend of an issue
often create indices of various values to track
progress. There is nothing intrinsically wrong
with using an index. They can have great
explanatory power. However, it's important to be
cautious of indices that combine disparate
measures.

For example, the United Nations
[Gender Inequality Index](http://hdr.undp.org/en/content/gender-inequality-index-gii)
combines several measures related to women's
progress toward equality. One of the measures used
in the GII is "representation of women in
parliament". Two countries in the world have laws
mandating gender representation in their
parliaments: China and Pakistan. As a result these
two countries perform far better in the index than
countries that are similar in all other ways. Is
this fair? It doesn't really matter, because it is
confusing to anyone who doesn't know about this
factor. The GII and similar indices should always
be used with careful analysis to ensure their
underlying variables don't swing the index in
unexpected ways.

### Results have been p-hacked

P-hacking is intentionally altering the data,
changing the statistical analysis, or selectively
reporting results in order to have statistically
significant findings. Examples of this include:
stop collecting data once you have a significant
result, remove observations to get a significant
result, or perform many analyses and only report
the few that are significant. There has been some
[good reporting](http://fivethirtyeight.com/features/science-isnt-broken)
on this problem.

If you're going to publish the results of a study
you need to understand what the p-value is, what
that means and then make an educated decision
about whether the results are worth using. Lots
and lots of garbage study results make it into
major publications because journalists don't
understand p-values.

เนื้อหาที่เกี่ยวข้อง:

- [Margin-of-error is too large](#margin-of-error-is-too-large)

### Benford's Law fails

[Benford's Law](https://en.wikipedia.org/wiki/Benford's_law)
is a theory which states that small digits (1,
2, 3) appear at the beginning of numbers much more
frequently than large digits (7, 8, 9). In theory
Benford's Law can be used to detect anomalies in
accounting practices or election results, though
in practice it can easily be misapplied. If you
suspect a dataset has been created or modified to
deceive, Benford's Law is an excellent first test,
but you should always verify your results with an
expert before concluding your data have been
manipulated.

### Too good to be true

There is no global dataset of public opinion.
Nobody knows the exact number of people living in
Siberia. Crime statistics aren't comparable across
borders. The US government is not going to tell
you how much fissile material it keeps on hand.

Beware any data that purport to represent
something that you could not possibly know. It's
not data. It's somebody's estimate and it's
probably wrong. Then again...it could be a story,
so ask an expert to check it out.

## ปัญหาที่คุณควรให้โปรแกรมเมอร์ช่วย

### ข้อมูลถูกสรุปรวบยอดมาผิดหมวดหมู่

Sometimes your data are at about the right level
of detail (neither
[too coarse](#data-are-too-coarse) nor
[too granular](#data-are-too-granular)), but they
have been aggregated to a different grouping than
you want. The classic example of this is data that
are aggregated by zip codes that you would prefer
to have by city neighborhoods. In many cases this
is an impossible problem to solve without getting
more granular data from your source, but sometimes
the data can be proportionally mapped from one
group to another. This must be undertaken only
with careful understanding of the
[margin-of-error](#margin-of-error-is-too-large)
that may be introduced in the process. If you've
got data aggregated to the wrong groups, ask a
programmer if it is possible to re-aggregate it.

เนื้อหาที่เกี่ยวข้อง:

- [Data are too coarse](#data-are-too-coarse)
- [Data are too granular](#data-are-too-granular)
- [Margin-of-error is too large](#margin-of-error-is-too-large)

### ข้อมูลถูกจัดเก็บอยู่ในเอกสารที่ถูกสแกน

ต้องขอบคุณกฏหมาย FOIA (The Freedom of Information Act ของประเทศสหรัฐอเมริกา) ที่กำกับให้รัฐบาลต้องเปิดเผยข้อมูลแม้เขาจะไม่ค่อยอยากเปิดข้อมูลก็ตาม
หลาย ๆ ครั้ง การไม่อยากเปิดเผยข้อมูลมาในรูปแบบของการเปิดเผยข้อมูลที่ยากต่อการเข้าถึงเช่น
การเปิดข้อมูลในรูปแบบภาพถ่ายของเอกสาร หรือ เอกสารที่ถูกสแกน หรือเอกสารที่จัดเก็บอยู่ไฟล์สกุล PDF

ถึงแม้ว่าเราจะสามารถดึงข้อความออกมาจากภาพ หรือไฟล์ PDF และแปลงกลับออกมาเป็นข้อมูลได้แล้วผ่านการใช้เทคโนโลยี optical-character recognition (OCR)
เทคโนโลยี OCR สมัยใหม่สามารถทำงานได้ถูกต้อง 100% แต่ส่วนใหญ่จะขึ้นอยู่กับคุณภาพของเอกสารต้นฉบับ ทำให้ทุก ๆ ครั้งที่มีการใช้ OCR เราจำเป็นจะต้องตรวจเช็คความเรียบร้อยกับต้นฉบับทุกครั้งก่อนนำไปใช้งาน

ในปัจจุบันมีหลายเว็บไซต์ ที่ให้บริการแปลงเอกสารเป็นข้อมูลผ่านการใช้เทคโนโนโลยี OCR (บางอันก็ฟรี) ควรปรึกษาโปรแกรมเมอร์เพิ่มเติม เพื่อเลือกใช้เครื่องมือให้เหมาะสม

เนื้อหาที่เกี่ยวข้อง:

- [ข้อมูลอยู่ในไฟล์ PDF](#ข้อมูลอยู่ในไฟล์-pdf)
