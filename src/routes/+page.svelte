<script>
    import {onMount} from 'svelte'
    import Kenya from './Kenya.svelte'
    let pathX=0;
    let pathY=0;
    let data={
        Nairobi:"13M",
        Wajir: "44M"
    }
    onMount(() => {
        let paths=document.querySelectorAll("path");
        paths.forEach(path=>{
            const div = document.querySelector('#bubble') || document.createElement('div');            
            path.addEventListener('mouseover', () => {
                // @ts-ignore
                const bubbletext= data[path.id] || 0
                div.textContent= `${path.id} ${bubbletext}` 
                paths.forEach(tmppath => {
                    tmppath.setAttribute("fill", "#D9D9D9")
                })
                path.setAttribute("fill", "red")
                pathX=path.getBoundingClientRect().x + path.getBoundingClientRect().width/2;
                pathY=path.getBoundingClientRect().y + path.getBoundingClientRect().height/2;
                if (path.parentNode) {
                    // @ts-ignore
                    div.style.position = "absolute";
                    // @ts-ignore
                    div.style.left =pathX + "px";
                    // @ts-ignore
                    div.style.top = pathY+ "px";
                }
            })
            path.addEventListener('mouseout',()=>{
                // div.remove();
            })
        })
    })
    
</script>

<Kenya></Kenya>
    
<div id="bubble" class=" h-10 rounded bg-red-300 text-white absolute z-50 p-1"></div>