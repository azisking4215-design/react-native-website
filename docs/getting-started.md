val NavyBlue = Color(0xFF1A3A8E)
val LightYellowBg = Color(0xFFFFFBEB)
val BorderColor = Color(0xFFE2E8F0)
val WarningText = Color(0xFFB45309)
@Composable
fun LaporanHarianScreen() {
    val scrollState = rememberScrollState()

    Column(
        modifier = Modifier
            .fillMaxSize()
            .background(Color(0xFFF8FAFC)) // Background abu muda
            .verticalScroll(scrollState)
    ) {
        // --- HEADER ---
        HeaderSection()

        Column(modifier = Modifier.padding(16.dp)) {
            // --- INPUT JUMLAH & HADIR ---
            Row(modifier = Modifier.fillMaxWidth(), horizontalArrangement = Arrangement.spacedBy(16.dp)) {
                CustomTextField(label = "Jumlah Personil", modifier = Modifier.weight(1f))
                CustomTextField(label = "Hadir", modifier = Modifier.weight(1f))
            }

            Spacer(modifier = Modifier.height(16.dp))

            // --- SECTION TIDAK HADIR (Kuning) ---
            Card(
                colors = CardDefaults.cardColors(containerColor = LightYellowBg),
                border = BorderStroke(1.dp, Color(0xFFFFE4A0)),
                shape = RoundedCornerShape(8.dp)
            ) {
                Column(modifier = Modifier.padding(16.dp)) {
                    Row(
                        modifier = Modifier.fillMaxWidth(),
                        horizontalArrangement = Arrangement.SpaceBetween,
                        verticalAlignment = Alignment.CenterVertically
                    ) {
                        Text("Tidak Hadir (Kurang)", fontWeight = FontWeight.Bold, color = WarningText)
                        Text("0", fontSize = 24.sp, fontWeight = FontWeight.Bold, color = WarningText)
                    }

                    Spacer(modifier = Modifier.height(12.dp))

                    // Grid untuk kategori absen
                    val categories = listOf("Cuti", "Izin Biasa", "Izin Lisan", "Sakit", "Piket", "Lepas Piket", "TL", "BKO", "TK")
                    
                    // Menggunakan FlowRow agar otomatis pindah baris (perlu dependency foundation layout)
                    FlowRow(
                        modifier = Modifier.fillMaxWidth(),
                        maxItemsInEachRow = 4,
                        horizontalArrangement = Arrangement.spacedBy(8.dp)
                    ) {
                        categories.forEach { label ->
                            SmallInputBox(label)
                        }
                    }
                }
            }

            Spacer(modifier = Modifier.height(16.dp))

            // --- KETERANGAN ---
            CustomTextField(
                label = "Keterangan",
                placeholder = "Contoh: BRIPDA John Doe - Sakit Demam",
                isSingleLine = false,
                modifier = Modifier.fillMaxWidth()
            )

            Spacer(modifier = Modifier.height(16.dp))

            // --- DROPDOWN KONDISI & CUACA ---
            Row(modifier = Modifier.fillMaxWidth(), horizontalArrangement = Arrangement.spacedBy(16.dp)) {
                DropdownField(label = "Kondisi Lapangan", value = "Kondusif", modifier = Modifier.weight(1f))
                DropdownField(label = "Cuaca", value = "Cerah", modifier = Modifier.weight(1f))
            }

            Spacer(modifier = Modifier.height(16.dp))

            // --- UPLOAD FOTO ---
            Text("Foto Dokumentasi (Wajib 2 Foto)", fontWeight = FontWeight.Bold, fontSize = 14.sp)
            Spacer(modifier = Modifier.height(8.dp))
            Row(modifier = Modifier.fillMaxWidth(), horizontalArrangement = Arrangement.spacedBy(16.dp)) {
                UploadBox("Foto 1", modifier = Modifier.weight(1f))
                UploadBox("Foto 2", modifier = Modifier.weight(1f))
            }

            Spacer(modifier = Modifier.height(24.dp))

            // --- TOMBOL KIRIM ---
            Button(
                onClick = { /* Handle Kirim */ },
                modifier = Modifier.fillMaxWidth().height(50.dp),
                shape = RoundedCornerShape(8.dp),
                colors = ButtonDefaults.buttonColors(containerColor = NavyBlue)
            ) {
                Icon(Icons.Default.CheckCircle, contentDescription = null, modifier = Modifier.size(18.dp))
                Spacer(Modifier.width(8.dp))
                Text("KIRIM LAPORAN HARIAN", fontWeight = FontWeight.Bold)
            }
            
            Spacer(modifier = Modifier.height(50.dp))
        }
    }
}
