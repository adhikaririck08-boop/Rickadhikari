val i = Intent(RecognizerIntent.ACTION_RECOGNIZE_SPEECH).apply {
  putExtra(RecognizerIntent.EXTRA_LANGUAGE_MODEL, "free_form")
  putExtra(RecognizerIntent.EXTRA_LANGUAGE, "bn-BD")
}
tts.language = Locale("bn", "BD")
fun handle(t: String) = when {
  "ইউটিউব" in t -> open("https://www.youtube.com/results?search_query=" + Uri.encode(t.substringAfter("গান")))
  "ফেসবুক" in t -> pkg("com.facebook.katana")
  "হোয়াটসঅ্যাপ" in t -> open("https://wa.me/88017XXXXXXXX?text=" + Uri.encode("হ্যালো"))
  "কল ধরো" in t -> (getSystemService(TELECOM_SERVICE) as TelecomManager).acceptRingingCall()
  else -> speak("বুঝতে পারিনি")
}
enum class Mood(val img: Int, val tone: Float) {
  HAPPY(R.drawable.rinki_happy, 1.2f), SAD(R.drawable.rinki_sad, 0.8f),
  ANGRY(R.drawable.rinki_angry, 1.0f), LOVE(R.drawable.rinki_love, 1.1f)
}
fun setMood(m: Mood) { avatar.setImageResource(m.img); tts.setPitch(m.tone) }
apk file download
