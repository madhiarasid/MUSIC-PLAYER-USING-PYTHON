# MUSIC-PLAYER-USING-PYTHON
import time
def create_playlist():
    songs = []
    num_songs = int(input("Enter the number of songs in your playlist: "))
    
    for i in range(num_songs):
        song_title = input(f"Enter song title ({i + 1}): ")
        songs.append(song_title)
    
    return songs

def play_song(song_list, current_song):
    global is_playing, is_paused

    if not is_playing or is_paused:
        print(f"Now playing: {song_list[current_song]}")
        is_playing = True
        is_paused = False

        # Simulate playback for a short duration
        for _ in range(5):
            print(".", end="")
            time.sleep(0.5)
        print("\n")

        if current_song < len(song_list) - 1:
            print(f"Next song: {song_list[current_song + 1]}")
    else:
        print(f"{song_list[current_song]} is already playing")

def pause_song(song_list, current_song):
    """Pauses playback and displays the paused song (if any)."""
    global is_paused, is_playing

    if is_playing and not is_paused:
        print(f"Pausing playback: {song_list[current_song]}")
        is_paused = True
    else:
        print("No song is playing to pause.")

def resume_song(song_list, current_song):
    """Resumes playback and displays the resumed song (if any)."""
    global is_paused, is_playing

    if is_paused:
        print(f"Resuming playback: {song_list[current_song]}")
        is_paused = False
    else:
        print("No song is paused to resume.")

def stop_song(song_list, current_song):
    """Stops playback and displays the stopped song (if any)."""
    global is_paused, is_playing

    if is_playing:
        print(f"Stopping playback: {song_list[current_song]}")
        is_paused = False
        is_playing = False
    else:
        print("No song is playing to stop.")
def next_song(song_list, current_song):
    """Selects the next song in the playlist."""
    if current_song < len(song_list) - 1:
        current_song += 1
        play_song(song_list, current_song)
    else:
        print("Reached the end of the playlist.")
    
    return current_song

def previous_song(song_list, current_song):
    """Selects the previous song in the playlist."""
    if current_song > 0:
        current_song -= 1
        play_song(song_list, current_song)
    else:
        print("Reached the beginning of the playlist.")
    
    return current_song

def main():
    song_list = create_playlist()
    current_song = 0
    
    global is_paused, is_playing
    is_paused = False
    is_playing = False

    while True:
        print("\nMusic Player")
        print("1. Play")
        print("2. Pause")
        print("3. Resume")
        print("4. Stop")
        print("5. Next Song")
        print("6. Previous Song")
        print("7. Exit")
        
        choice = input("Enter your choice (1-7): ")
        if choice == '1':
            play_song(song_list, current_song)
        elif choice == '2':
            pause_song(song_list, current_song)
        elif choice == '3':
            resume_song(song_list, current_song)
        elif choice == '4':
            stop_song(song_list, current_song)
        elif choice == '5':
            current_song = next_song(song_list, current_song)
        elif choice == '6':
            current_song = previous_song(song_list, current_song)
        elif choice == '7':
            print("Exiting Music Player.")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()

