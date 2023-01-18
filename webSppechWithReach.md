```
import React, { useState, useEffect } from 'react';

function TextToSpeech() {
  const [text, setText] = useState('');
  const [isSpeaking, setIsSpeaking] = useState(false);

  useEffect(() => {
    if (!window.speechSynthesis) {
      alert('Your browser does not support the Web Speech API');
      return;
    }
  }, []);

  function handleTextChange(e) {
    setText(e.target.value);
  }

  function speak() {
    if (!text) {
      return;
    }

    setIsSpeaking(true);

    const speech = new SpeechSynthesisUtterance();
    speech.text = text;

    window.speechSynthesis.speak(speech);

    speech.addEventListener('end', () => {
      setIsSpeaking(false);
    });
  }

  return (
    <>
      <textarea onChange={handleTextChange} value={text} />
      <button onClick={speak} disabled={isSpeaking}>
        Speak
      </button>
    </>
  );
}

export default TextToSpeech;
```