// masukkan TOKEN BOT dari BOT Father
const token = '5328310433:AAHxugsxGE3w_Drs_ISSecF3ricoWzFJXI4'

const tg = new telegram.daftar(token)

// masukkan ID kamu, jika belum tau cek di @strukturbot
const adminBot = 5097348378

// jika debug true, akan mengirimkan struktur JSON ke admin bot
const debug = false

// -- fungsi telegram

// cek informasi bot
function getMe() {
  let me = tg.getMe()
  return Logger.log(me)
}

function setWebhook() {
  var url = "https://script.google.com/macros/s/AKfycbxaOR1NMV4lM4os2P7fmTDvTtiL8wHxISoponv9ttBUUw8VGM8Iw8BX7h2tJ-fsYvd7mQ/exec"
  var r = tg.setWebhook(url)
  return Logger.log(r)
}

// cek info hook bot
function getWebhookInfo() {
  let hasil = tg.getWebhookInfo()
  return Logger.log(hasil)
}

// hapus hook
function deleteWebhook() {
  let hasil = tg.deleteWebhook()
  return Logger.log(hasil)

}

// -- kalau mau bikin fungsi sendiri, taruh di bawah sini ---


proses


// fungsi buat handle hanya menerima pesan berupa POST, kalau GET keluarkan pesan error
function doGet(e) {
  return tg.util.outputText("Hanya data POST yang kita proses yak!");
}

// fungsi buat handle pesan POST
function doPost(e) {
  // data e kita verifikasi
  let update = tg.doPost(e);

  try {
    if (debug) return tg.sendMessage(adminBot, JSON.stringify(update, null, 2))
    prosesPesan(update)
  } catch (e) {
    tg.sendMessage(adminBot, e.message)
  }

}

// fungsi utama untuk memproses segala pesan yang masuk
function prosesPesan(update) {

  // deteksi tipe message
  if (update.message) {

    // penyederhanaan variable
    var msg = update.message;

    // deteksi event letakkan di sini
    if (msg.new_chat_members) {
      var newUser = msg.new_chat_members[0];

      var nama = newUser.first_name;
      if (newUser.last_name)
        nama += " " + newUser.last_name;

      //rangkai ucapan welcome
      var teks = "Selamat datang, bos <b>" + nama + "</b>. \nšš»āāļø berikut event kami yang masih berjalan ya bos ku š„ \n\nā=SLOT=ā \nš°	BONUS JACKPOT FREE SPIN MURNI 25%šØ \nš° BONUS JACKPOT BUY SPIN 15%šØ \nš° BONUS  DEPOSIT 10% SETIAP HARIšØ \n\nā=SPORTSBOOK=ā \nā½ CASHBACK BOLA 10%šØ \nā½ EVENT WIN STREAKšØ \nā½ XTRA WIN PARLAYšØ \nā½ CASHBACK PARLAY 100%šØ \nā½ KOMPETISI PARLAY 5 TEAM šØ<b>SETIAP HARI</b>šØ \n\nā=CASINO=ā \nš² LUCKY TICKET CASINOšØ \nš² WIN STREAK CASINOšØ \n\nUntuk <b>POLA</b> Ke <b>REAL ADMIN</b> ya bos ku \n\nSyarat dan ketentuan EVENT bisa klick di bawah ini ya bos \nššššššššššš \nš° /SLOT šØ \nā½ /BOLA šØ \nš² /CASINO šØ \nā  /POKER šØ \nš± /TOGEL šØ \nšØ /GACOR š¢";

      var keyboard = []

        // keyboard baris pertama
        // index dimulai dari 0
        keyboard[0] = [
          tg.button.url('šÆ Link Daftar š¦', 'https://magic.ly/info_slot'),
          tg.button.url('š„ REAL ADMIN', 'https://t.me/csindoacejessica'),
        ];

        keyboard[1] = [
          tg.button.url('š Whatsapp š', 'https://wa.me/6281291093447'),
        ];

      // kirim pesan welcome
      return tg.sendMsgKeyboardInline(msg, teks, keyboard, 'HTML');
      
    }

    // jika ada pesan berupa text
    if (msg.text) {

      // jika user klik start, bot akan menjawab
      var pola = /\/event/i
      if (pola.exec(msg.text)) {
        var nama = msg.from.first_name
        if (msg.from.last_name)
          nama += ' ' + msg.from.last_name
        // perhatikan, ini menggunakan sendMsg bukan sendMessage
        var pesan = "šš½ Halo, <b>" + tg.util.clearHTML(nama) + "</b>, \nš  <b>INFO EVENT PROMO BONUS BO INDOACE</b> ā \n\nšš»āāļø berikut event kami yang masih berjalan ya bos ku š„ \n\nā=SLOT=ā \nš°	BONUS JACKPOT FREE SPIN MURNI 25% šØ \nš° BONUS JACKPOT BUY SPIN 15% šØ \nš° BONUS  DEPOSIT 10% SETIAP HARI šØ \n\nā=SPORTSBOOK=ā \nā½CASHBACK BOLA 10% šØ \nā½ EVENT WIN STREAK šØ \nā½ XTRA WIN PARLAY šØ \nā½ CASHBACK PARLAY 100% šØ \nā½ KOMPETISI PARLAY 5 TEAM šØ <b>SETIAP HARI</b> šØ \n\nā=CASINO=ā \nš² LUCKY TICKET CASINO šØ \nš² WIN STREAK CASINO šØ \n\nā=POKER & TOGEL=ā \nā  BONUS KOMISI 0,3% šØ Untuk <b>POLA</b> Ke <b>REAL ADMIN</b> ya bos ku \n\nuntuk syarat dan ketentuan klick di bawah ini ya bos \nššššššššššš \nš° /SLOT šØ \nā½ /BOLA šØ \nš² /CASINO šØ \nā  /POKER šØ \nš± /TOGEL šØ \nšØ /GACOR š¢"

        var keyboard = []

        // keyboard baris pertama
        // index dimulai dari 0
        keyboard[0] = [
          tg.button.url('šÆ Link Daftar š¦', 'https://magic.ly/setting_slot'),
          tg.button.url('š„ REAL ADMIN', 'https://t.me/csindoacejessica'),
        ]

        keyboard[1] = [
          tg.button.url('š Whatsapp š', 'https://wa.me/6281291093447'),
        ]

        return tg.sendMsgKeyboardInline(msg, pesan, keyboard, 'HTML')
      }

      // jika user ketik /ping, bot akan jawab Pong!
      // pola dan jawaban paling sederhana
      var pola = /^[\/!]ping$/i
      if (pola.exec(msg.text)) {
        // balas pong dengan mereply pesan
        // menggunakan parse_mode Markdown
        return tg.sendMessage(msg.chat.id, 'š hallo bos, untuk info bisa klik /start atau /event ya bos ku \nJessica hanya menginfokan event promo bonus BO INODACE saja ya bos', 'Markdown', false, false, msg.message_id)
      }


      // jika user ketik /pong, sekalian dihitung selisihnya
      // dan diberikan berbagai contoh kasus

      // balas pong dengan mereply pesan
      // menggunakan parse_mode Markdown
      var pola = /^[\/!]Gacor/i
      if (pola.exec(msg.text)) {

        // awal waktu pakai timestampnya message saja
        // jika bot macet timestamp pengirim tetap diperhitungkan
        // pilihan lain bisa bikin time sendiri
        var waktuAwal = msg.date
        var hasil = tg.sendMessage(msg.chat.id, '<b>Gacor</b>', 'HTML', false, false, msg.message_id)

        var newMsg = hasil.result
        var waktuAkhir = new Date()

        let Gacor = [
          'https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhlOiTL2yspyBIOtKK7ehb3qg3GmvvTBbv1_i2hCODG52nGYNKSGCU_YTJDY655b47AjMCdJzzEQQBxxk5cgyUWrhMiOrSRrozmrrYpze0pR514ddtZ0tWjftawPtRGG6BgV6Yg4o77ooFzxuESjBm483emQ02tDQIo6K6xTLuX6Df7JIda0EYpXZuK/s1600/3.jpg',
          'https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjEyCP8u98rCK8bXS9jfHGyRKJLO_NWRc5H8mJVxT1_zVuk6iQ_tsnGFNIn6_pe3XIo57PGPJL-4B2epcvN62ok_PcXB3yW1Xaa-jEvxwSuBRi1ZM4GB9nsepbWCAFGM-Oz5vVlnB2BQEXB5KGm32SkbF8zflYDh3mr1Dxv3gAJdxB0gA--jot_f7z2/s1600/4.jpg',
          'https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhsgCcSPeQj0_Go5Uj0-Ykd2lvWzK0J06agmSgBH1eG4HtwCXf7L0FSbaRZ8IuDExP1se4_yvn-MsQsEi2Jmn7v6tyUv5qKQU7SHLnWdtPjvfC9wVLzJEUzD1lXVVFlnwRpa_SY2QTNAZqbV9uiCdJjhgPEeLFrdeKgqSULwnGerDU5h2HVBIBggmPT/s1600/5.jpg',
          'https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiU6H2uQGv7IqwcaMJRJGBhWPbqm1-hiqujkIekyVYxSctmqP4tcjumd-SgxvXCZI6Pz14VKthJnNN21Qubw06cZPQIW_T0tnDgCE4kQ0gBaDQXHdZ6IMhNMX0Ywq6kYpOgenZ5KdWTWY5Cz1p71ApITGthp7_c0oj0q_f5skRSatksjJNMj_mxf4S5/s1600/slot1.jpg',
          'https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEiwQFExhmgBo5b4d8DtpxCNhXFc0E-s_XGFj2wxerAormYgq_SkCEGX0m9UMbDyeKvcfiSkECOmcRzu_zpooIv7OCRjcsLaeeiH8OrhGKcZ1TaLQI-gfvVahHWSkFCd5KDpxP4mXNngBYtKy6KgeIrrd0qvhi3t9nKuIMrm4PMdCQyXlKW3Vrlurxa6/s1600/slot2.jpg'
        ]

        // foto gambar disembunyikan di emoticon mie
        var pesan = '<a href="' + tg.util.random(Gacor) + '">šØ</a> '
        pesan += `š£<b>Gas bos ku</b>.\nā” Untuk trik dan pola nya chat langsung ke \nREAL ADMIN kami ya bos @csindoacejessica.`

        return tg.editMessageText(msg.chat.id, newMsg.message_id, false, pesan, 'HTML')
      }

      // kirim foto dari URL
      var pola = /^[\/!](slot)/i
      if (cocok = pola.exec(msg.text)) {
        var url = 'https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEimGa1MIALgN6oyfwpdyFDWBryNuoAmGzOGtUXx8EQEKwbVT_p6VOb1QDutWu0RBBTXhb2vxNyVBH7tcDzHwXQUkT2wM8-J7VbO7_BUg4_OY0pFWSzEePaEYQGEG1WTirR_n0gAMDC6JRFBk4njbGblWJ6kO8TKBz5YiQ6av3WV_jyOlDae5V6_irF0/s1200/s&amp;k%20slot.jpg'
        var caption = 'Syarat & Ketentuan: š° EVENT SLOT š° \nUntuk INFO lebih lanjut chat ke ADMIN kami ya bos @csindoacejessica'
        return tg.sendPhoto(msg.chat.id, url, caption, 'HTML')
      }

      // kalau mau kembangin sendiri menjadi bot interaktif, code nya taruh di bawah ini
      // -- mulai custom deteksi text --

      var pola = /^[\/!](bola)/i
      if (cocok = pola.exec(msg.text)) {
        var url = 'https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEgkBclkki2Xq0ujuUt_fNMHBdIP5S2yuQPhg68j6PuFOCMMmpdf7FXK6UPvJSFlcbER1mdgwTaaKsB3uqRHTuiEazhDsMiZum5dTWc0L3UR_WWxP76Pie2mXOQvDjHPG8clwyFc55tVnXq36tZoHxCELQrl42MJpLe0RJXqiL9dvp52AIkCjAO7PVAI/s16000/BOLA.jpg'
        var caption = 'Syarat & Ketentuan: ā½ EVENT BOLA ā½ \nUntuk INFO lebih lanjut chat ke ADMIN kami ya bos @csindoacejessica'
        return tg.sendPhoto(msg.chat.id, url, caption, 'HTML')
      }

      var pola = /^[\/!](casino)/i
      if (cocok = pola.exec(msg.text)) {
        var url = 'https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhXC_XD4Y1Q2MdT49UwAQWR9BuhWchofTR3yEuwe6_2mBDJCxW9O71dBvp8wuxSNnG9VmUCn69MOycKnf8WIH-qex7Zb8QxgPsP4wyU_7ZupjOM7pOR7onAS0VhRZLfp48FXCnOgrloF7kdUqkovHkhYUbun1GROmSI5yFjcks_s0zDqui8ewv50chY/s16000/casino2.jpg'
        var caption = 'Syarat & Ketentuan: š² EVENT CASINO š² \nUntuk INFO lebih lanjut chat ke ADMIN kami ya bos @csindoacejessica'
        return tg.sendPhoto(msg.chat.id, url, caption, 'HTML')
      }

      var pola = /^[\/!](poker)/i
      if (cocok = pola.exec(msg.text)) {
        var url = 'https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhMnUWSFyjR7hKM4xY0MoXgiKhFdD6rufOSK-ILQfpmz3nFBWcJEV9LU5E1-XTcTg37XDuDn8nFBv6t3jZWEGDO8FdG_bd-b272dTCs-zTuuSFsLfDE5vm5eOP3snzfTdhgbbrVr6PQQH-DHdaARCyIFUTG9d7aTkdMfQ3cxsJALKXHDsmzja2_xEus/s16000/poker%20togel.jpg'
        var caption = 'Syarat & Ketentuan: ā  EVENT POKER DAN TOGEL š± \nUntuk INFO lebih lanjut chat ke ADMIN kami ya bos @csindoacejessica'
        return tg.sendPhoto(msg.chat.id, url, caption, 'HTML')
      }

      var pola = /^[\/!](togel)/i
      if (cocok = pola.exec(msg.text)) {
        var url = 'https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhMnUWSFyjR7hKM4xY0MoXgiKhFdD6rufOSK-ILQfpmz3nFBWcJEV9LU5E1-XTcTg37XDuDn8nFBv6t3jZWEGDO8FdG_bd-b272dTCs-zTuuSFsLfDE5vm5eOP3snzfTdhgbbrVr6PQQH-DHdaARCyIFUTG9d7aTkdMfQ3cxsJALKXHDsmzja2_xEus/s16000/poker%20togel.jpg'
        var caption = 'Syarat & Ketentuan: ā  EVENT POKER DAN TOGEL š± \nUntuk INFO lebih lanjut chat ke ADMIN kami ya bos @csindoacejessica'
        return tg.sendPhoto(msg.chat.id, url, caption, 'HTML')
      }

      // akhir deteksi pesan text
    }

    // akhir update message
  }

  // deteksi callback
  if (update.callback_query) {
    // proses di halaman berikutnya, biar gak terlalu panjang     
    return prosesCallback(update.callback_query)
  }

}
