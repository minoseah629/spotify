# spotify

This project is a starter project to migrate from previous music provider to Spotify.  

# Dataset
In the My Thumbup csv, there are 3 columns: name (of track), artist, and album. Id is in csv, but not useful.

<img width="1230" alt="image" src="https://github.com/minoseah629/spotify/assets/1980068/e0891ada-6dc3-4a7f-ab1c-ea0a25435862">

# Tools 
python, pandas, spotify web api (attempted to use spotipy, but struggled), dotenv, microsoft iis (only to get authorization code back Spotify API)

# Methodology

1. Created a Spotify Application 
2. Established environmental variables for spotify client id and secret using .dotenv file
3. Establish local webserver (iis)
4. read csv with pandas
5. Authorize API connections using `https://accounts.spotify.com/authorize`
   * Reference: https://developer.spotify.com/documentation/web-api/tutorials/code-flow
6. Retrieved code and state from response of `https://accounts.spotify.com/authorize`
   <img width="485" alt="image" src="https://github.com/minoseah629/spotify/assets/1980068/c697f276-f8a6-4bb0-b7b6-6898fc75718c">
   * Code is no longer valid
8. Initiated token request using `https://accounts.spotify.com/api/token` with basic authenication
9. Initiated Spotify API for user information using `https://api.spotify.com/v1/me/`
   * For user id 121308190
10. Create new playlist using Spotify API for user information using `https://api.spotify.com/v1/users/{user_id}/playlists`
11. Create query string with track and artist
12. Iterated on csv to query Spotify API if song is available in Spotify Library `https://api.spotify.com/v1/search?q={query}&type=track&limit=1`
13. If query response was successful and query response had tracks > items > 0 (first item) > get ID of song
14. Track list of songs up to 100 songs (`https://api.spotify.com/v1/playlists/{playlist['id']}/tracks` accepted 100 tracks at a time)
15. Add current iteration of 100 tracks to playlist
16. Repeat until finished last 100 songs
17. Add last iteration of tracks less than 100 to playlist
