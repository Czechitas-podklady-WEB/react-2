## Přehrávání audia/videa

Dalším případem, kdy se nám v Reactu hodí hook `useRef` může být přehrávání audia či videa. HTML elementy `audio` a `video` jsou postavené tak, že k jejich ovládní je třeba volat různé metody jako `play()`, `pause()` a podobně. V Reactu tak opět potřebujeme přístup k DOM elementu skrze `useRef`. 

Jako ukázku si vyrobíme tedy jednoduchou komponentu `MusicPlayer`, která bude zatím obsahovat pouze tlačítko na spuštění a zastavení přehrávání. Jako soubor k přehrávání použijeme skladbu s názvem [Meaning](assets/vlad-gluschenko-meaning.mp3).

```jsx
const MusicPlayer = ({ src }) => {
  const [playing, setPlaying] = useState(false);
  const audioRef = useRef();

  useEffect(() => {
    if (playing) {
      audioRef.current.play();
    } else {
      audioRef.current.pause();
    }
  }, [playing]);

  const handlePlay = () => {
    setPlaying(!playing);
  };

  return (
    <div className="music-player">
      <audio ref={audioRef} src={src} />
      <button onClick={handlePlay}>{playing ? 'stop' : 'play'}</button>
    </div>
  );
};
```