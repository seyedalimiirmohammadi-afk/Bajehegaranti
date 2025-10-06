<!DOCTYPE html>
<html lang="fa">
<head>
<meta charset="UTF-8">
<title>فرم آنلاین گارانتی دستگاه</title>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>
<style>
body { font-family: Tahoma, sans-serif; direction: rtl; padding: 20px; }
label { display: block; margin-top: 10px; }
input, select { width: 300px; padding: 5px; margin-top: 5px; }
button { margin-top: 20px; padding: 10px 20px; }
</style>
</head>
<body>

<h2>فرم آنلاین قرارداد گارانتی دستگاه</h2>

<label>نام و نام خانوادگی مسئول باجه:</label>
<input type="text" id="name" required>

<label>کد باجه:</label>
<input type="text" id="code" required>

<label>کد ملی مسئول باجه:</label>
<input type="text" id="national" required>

<label>آدرس باجه:</label>
<input type="text" id="address" required>

<label>شماره تماس:</label>
<input type="text" id="phone" required>

<label>مدل دستگاه:</label>
<select id="model">
  <option value="Evolis PPL4">Evolis PPL4</option>
  <option value="Evolis Dualys 3">Evolis Dualys 3</option>
  <option value="Qb10">Qb10</option>
  <option value="Hodo">Hodo</option>
  <option value="Smart 50">Smart 50</option>
  <option value="Smart 51">Smart 51</option>
</select>

<label>سطح گارانتی:</label>
<select id="level">
  <option value="Gold">طلایی</option>
  <option value="Silver">نقره‌ای</option>
  <option value="Bronze">برنزی</option>
</select>

<label>بارگذاری عکس دستگاه (اجباری):</label>
<input type="file" id="devicePhoto" accept="image/*" required>

<label>رسید پرداخت مرحله اول:</label>
<input type="text" id="receipt" required>

<label>مبلغ گارانتی:</label>
<input type="text" id="price" readonly>

<button onclick="generatePDF()">تولید PDF قرارداد</button>

<script>
// جدول قیمت‌ها
const prices = {
  "Evolis PPL4": { Gold: 4000000, Silver: 3600000, Bronze: 3240000 },
  "Evolis Dualys 3": { Gold: 4000000, Silver: 3600000, Bronze: 3240000 },
  "Qb10": { Gold: 4000000, Silver: 3600000, Bronze: 3240000 },
  "Hodo": { Gold: 2000000, Silver: 1900000, Bronze: 1805000 },
  "Smart 50": { Gold: 5000000, Silver: 4500000, Bronze: 4050000 },
  "Smart 51": { Gold: 6000000, Silver: 5400000, Bronze: 4860000 }
};

const modelSelect = document.getElementById('model');
const levelSelect = document.getElementById('level');
const priceInput = document.getElementById('price');

function updatePrice() {
  const model = modelSelect.value;
  const level = levelSelect.value;
  priceInput.value = prices[model][level].toLocaleString() + " تومان";
}

modelSelect.addEventListener('change', updatePrice);
levelSelect.addEventListener('change', updatePrice);
updatePrice();

function generatePDF() {
  const { jsPDF } = window.jspdf;
  const doc = new jsPDF({ orientation: "portrait" });

  const name = document.getElementById('name').value;
  const code = document.getElementById('code').value;
  const national = document.getElementById('national').value;
  const address = document.getElementById('address').value;
  const phone = document.getElementById('phone').value;
  const model = modelSelect.value;
  const level = levelSelect.value;
  const price = priceInput.value;
  const receipt = document.getElementById('receipt').value;

  if (!name || !code || !national || !address || !phone || !receipt || !document.getElementById('devicePhoto').files[0]) {
    alert("لطفاً تمام فیلدها را تکمیل کنید و عکس دستگاه را بارگذاری نمایید.");
    return;
  }

  const photoFile = document.getElementById('devicePhoto').files[0];
  const reader = new FileReader();
  reader.onload = function(e) {
    doc.setFont("Tahoma");
    doc.setFontSize(12);
    doc.text("قرارداد اینترنتی گارانتی دستگاه‌های صدور کارت", 105, 10, null, null, "center");
    doc.text(`نام مسئول باجه: ${name}`, 10, 30);
    doc.text(`کد باجه: ${code}`, 10, 40);
    doc.text(`کد ملی مسئول باجه: ${national}`, 10, 50);
    doc.text(`آدرس باجه: ${address}`, 10, 60);
    doc.text(`شماره تماس: ${phone}`, 10, 70);
    doc.text(`مدل دستگاه: ${model}`, 10, 80);
    doc.text(`سطح گارانتی: ${level}`, 10, 90);
    doc.text(`مبلغ گارانتی: ${price}`, 10, 100);
    doc.text(`رسید پرداخت مرحله اول: ${receipt}`, 10, 110);
    doc.text("گارانتی تنها پس از بارگذاری عکس دستگاه و تایید پرداخت فعال می‌گردد.", 10, 120);
    doc.addImage(e.target.result, 'JPEG', 10, 130, 50, 50);
    doc.save(`Garanti_${model}_${name}.pdf`);
  };
  reader.readAsDataURL(photoFile);
}
</script>

</body>
</html>
