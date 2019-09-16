$(document).ready(function () {

    console.log("READY!");

    // spotify api
    // access token (for ajax call)

    var clientId = '090007e3600d4e579a27e68795279b6d'; // Your client id
    
    // var client_secret = '7d841303f464421cb70cb9524f045734'; // Your secret

    // window.onSpotifyWebPlaybackSDKReady = () => {
    //     var token = "BQAijHyFMOA1uensNTaFjPvtRD9hRBLL6gsHGxuCyYcQYB6zxJcuDqw48g4QUoBCfOAO6frdRJK2Y3k14uCvFQsafXffZzjkD9s1YM9Rna7pil50x5_Y-kg0MNCAgVZgn5nrER26JSVWWRMh61ni2TZ5PpuotLLFMiHX29zsn1R6aa2XfY9DGA";
    //     const player = new Spotify.Player({
    //         name: 'Web Playback SDK Quick Start Player',
    //         getOAuthToken: cb => {
    //             cb(token);

    //         }
    //     });
    // }
 
    //     // Get the hash of the url
    //     const hash = window.location.hash
    //     .substring(1)
    //     .split('&')
    //     .reduce(function (initial, item) {
    //     if (item) {
    //         var parts = item.split('=');
    //         initial[parts[0]] = decodeURIComponent(parts[1]);
    //     }
    //     return initial;
    //     }, {});
    //     window.location.hash = '';
    
        // Set token
        let _token = 'BQAB3arRjoeeUQ45d1La2xs-zZkN0MybJcDEHDD6TZbrPsySKnJ6e6qtTRF-y92SLig9PM0s2JBRGzvvsbvwp8hy6HKK3TwsMfCkTrNx9w3XsJvIRzxiTKky4wAMeChK-pLyDZzws2le6AgufxfxYEOy7L18ahCv-bDJoBmKs2GFu85HNUlwTw';

        


    
        const authEndpoint = 'https://accounts.spotify.com/authorize';
    
        // Replace with your app's client ID, redirect URI and desired scopes
         clientId = '04e15c5176114e1fb2ebc700280292ee';
        const redirectUri = 'music-project-login://callback';
        const scopes = [
            'streaming',
            'user-read-birthdate',
            'user-read-private',
            'user-modify-playback-state',
            'user-read-playback-state'
        ];
    
        // If there is no token, redirect to Spotify authorization
        if (!_token) {
            window.location = `${authEndpoint}?client_id=${clientId}&redirect_uri=${redirectUri}&scope=${scopes.join('%20')}&response_type=token&show_dialog=true`;
        }
    
        // Set up the Web Playback SDK
    
        window.onSpotifyPlayerAPIReady = () => {
            const player = new Spotify.Player({
                name: 'Web Playback SDK Template',
                getOAuthToken: cb => { cb(_token); }
            });
    
            // Error handling
            player.on('initialization_error', e => console.error(e));
            player.on('authentication_error', e => console.error(e));
            player.on('account_error', e => console.error(e));
            player.on('playback_error', e => console.error(e));
    
            // Playback status updates
            player.on('player_state_changed', state => {
                console.log(state)
                var currentTrack = $('#current-track').text('src', state.track_window.current_track.album.images[0].url);
                currentTrack.html();
                var currentTrackName = $('#current-track-name').text(state.track_window.current_track.name);
                currentTrackName.html();
            });

          
            // Ready
            player.on('ready', data => {
                console.log('Ready with Device ID', data.device_id);
                
                // Play a track using our new device ID
                device_id = data.device_id;

                 play(data.device_id);

            });
    
            // Connect to the player!
            player.connect();
        }
        var device_id = "";
        // Play a specified track on the Web Playback SDK's device ID
        function play(device_id) {
        $.ajax({
        url: "https://api.spotify.com/v1/play/device_id?" + device_id,
        type: "curl -X PUT https://api.spotify.com/v1/me/player/play?",
        data: '{"uris": ["spotify:track:2YpeDb67231RjR0MgVLzsG]}',
        beforeSend: function(xhr){xhr.setRequestHeader('Authorization', 'Bearer ' + _token );},
        success: function(data) { 
            console.log(data)

        }
        });
        }
  
    $("#spotify").on('click', function (event) {
        event.preventDefault();
        console.log("button is clicked");
        
        // $("<audio>").append('<source>' + [data.tracks.item[0].id] + '</source>'); 
        $(".jumbotron").show();
        var searchValue = $("#searchBox").val();

        var _token = "BQAB3arRjoeeUQ45d1La2xs-zZkN0MybJcDEHDD6TZbrPsySKnJ6e6qtTRF-y92SLig9PM0s2JBRGzvvsbvwp8hy6HKK3TwsMfCkTrNx9w3XsJvIRzxiTKky4wAMeChK-pLyDZzws2le6AgufxfxYEOy7L18ahCv-bDJoBmKs2GFu85HNUlwTw";

        $.ajax({
            type: "GET",
            url: "https://api.spotify.com/v1/search?q=" + searchValue + "&type=track",
            headers: {
                'Authorization': 'Bearer ' + _token
            },
            data: {
                'context_uri': 'spotify:track:2iCcqggir1VUNIHfKDYKX9',
                'position_ms': 5000
            },
            success: (data)=>{
                console.log(data);
               play(data.tracks.items[0].id);
               
           }
        })
        
    });
 

    // bands in town api for events //

    var bands = $("#bandsInTown").html();

    var appID = "appId=369ee177bec3664bb630131b48ca0627"
    var queryUrl2 = "rest.bandsintown.com" + appID;

    var artistName = $("#searchBox").html();

    $.ajax({
        url: "https://cors-anywhere.herokuapp.com/ " + queryUrl2,
        method: "GET /artists/" + artistName + "/events",
    }).then(function () {

        bands.show();



    });

});

