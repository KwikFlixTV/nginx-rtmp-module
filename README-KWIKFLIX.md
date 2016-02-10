### New Features

* HLS Ability to cut of last N segments from index files thus producing delay for (N * segment duration) seconds;

### Usage

`hls_cut_fragments X;` - where X number of segments to cut

### Example nginx.conf

Following will produce 30 seconds delay:

    rtmp {
        server {
            listen 1935;
            ping 30s;
            play_restart on;

            application live {
                live on;
                hls on;
                hls_path /home/redhat/nginx-rtmp-vod/hls;
                hls_nested on;
                hls_continuous on;
                hls_fragment 1s;
                hls_playlist_length 1m;
                hls_fragment_slicing aligned;
                hls_cut_fragments 30;
            }
         }
    }
