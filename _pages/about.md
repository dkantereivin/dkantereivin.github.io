---
permalink: /
title: "Welcome to my Academic Website!"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

Hi there! I'm David Kanter Eivin, a final year medical student at McMaster University's Niagara Regional Campus. This is a personal academic website for showcasing my research and academic work.

My research interests include:
- **Artificial Intelligence in Medicine**: Exploring the use of LLMs for systematic reviews, as well as the integration of AI into medical curricula through formal teaching and student-led initiatives.
- **Health Systems Research**: Utilizing geospatial analysis and large-scale datasets to investigate physician distribution and access to care across Canada.
- **Emergency Department Flow**: Understanding factors affecting throughput of patients through the ED, including disposition prediction, and integration of technology to streamline care.
- **Epigenetic Aging**: Investigating the use of epigenetic biomarkers for outcome prediction in ICU patients and in sepsis.

I also have broad clinical interests in particular with emergency medicine, critical care, and pre-hospital/transport medicine.

While I'm sure that all sounds *riveting*, in my free time I'm a huge outdoors person. I enjoy hiking, camping, skiing, sailing. I'm a nerd for strategy games, and I'm always up for a board game night with friends: Puerto Rico, Taboo, Ticket to Ride (and various card games) are favorites. When I can I also indulge in video games -- my favorites are *The Long Dark*, *Civilization*, *Anno 1800*, and *Cities: Skylines*. When I’m not at a screen or a table (or in the hospital), I'm trying to travel wherever I can, chefing up a fancy brunch, or spending time with friends and family.

Oh, and I'm a movie star 🎥... well, more that I was featured in McMaster's Niagara Campus video. Check it out [here](https://ugme.healthsci.mcmaster.ca/about-us/our-campuses/niagara-regional-campus/).


Many of the details of this site are still a work in progress, but you can view some of my research papers, projects, and other academic contributions. Alternatively, for a more complete overview of my previous works,
you can view my CV [here](/files/cv/em.pdf).

Please feel free to contact me if you have any questions or if you're interested in collaborating on research projects.

### Gallery

<div id="immich-frame" style="width: 100%; max-width: 800px; height: 500px; margin: 0 auto; position: relative; border-radius: 10px; overflow: hidden; box-shadow: 0 4px 12px rgba(0,0,0,0.15); background: #f0f0f0;">
    <img id="frame-image" src="" alt="Loading gallery..." style="width: 100%; height: 100%; object-fit: cover; transition: opacity 1s ease-in-out; opacity: 0;">
    <div style="position: absolute; bottom: 10px; right: 10px; background: rgba(0,0,0,0.5); color: white; padding: 5px 10px; border-radius: 20px; font-size: 12px; pointer-events: none;">
        <span id="photo-credit">Immich Gallery</span>
    </div>
</div>

<script>
    const CONFIG = {
        domain: "https://immich.kantereivin.ca",
        shareKey: "dkanter_public", // The part after /s/ in your URL
        interval: 5000 // Time per slide in ms
    };

    async function startSlideshow() {
        try {
            // 1. Fetch the assets from the shared link API
            // Correct endpoint for public shares: /api/shared-links/me?slug={shareKey}
            const response = await fetch(`${CONFIG.domain}/api/shared-links/me?slug=${CONFIG.shareKey}`, {
                headers: { 'Accept': 'application/json' }
            });
            const data = await response.json();
            const assets = data.assets;
            
            if (!assets || assets.length === 0) return;

            const imgElement = document.getElementById('frame-image');
            let currentIndex = 0;

            // 2. Function to update the image
            const showNextImage = () => {
                const asset = assets[currentIndex];
                // Construct the asset URL
                // Use 'slug' parameter for public access
                const imageUrl = `${CONFIG.domain}/api/assets/${asset.id}/thumbnail?size=preview&slug=${CONFIG.shareKey}`;
                
                // Preload next image for smoothness
                const nextIndex = (currentIndex + 1) % assets.length;
                const nextAsset = assets[nextIndex];
                const nextUrl = `${CONFIG.domain}/api/assets/${nextAsset.id}/thumbnail?size=preview&slug=${CONFIG.shareKey}`;
                new Image().src = nextUrl;

                // Fade out, switch source, fade in
                imgElement.style.opacity = 0;
                setTimeout(() => {
                    imgElement.src = imageUrl;
                    imgElement.onload = () => { imgElement.style.opacity = 1; };
                }, 1000); // Matches CSS transition time

                currentIndex = nextIndex;
            };

            // Start loop
            showNextImage();
            setInterval(showNextImage, CONFIG.interval);

        } catch (e) {
            console.error("Could not load Immich gallery:", e);
            document.getElementById('immich-frame').innerHTML = "<p style='text-align:center; padding-top:40%; color:#666;'>Gallery currently unavailable.</p>";
        }
    }

    document.addEventListener("DOMContentLoaded", startSlideshow);
</script>