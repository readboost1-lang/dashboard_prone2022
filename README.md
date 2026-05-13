<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>Dashboard PRONEs CNC 2022</title>
<style>
*{box-sizing:border-box;margin:0;padding:0}
body{background:#0A1520;font-family:system-ui,sans-serif;color:#CBD5E1;padding:10px}
.wrap{background:#0F1923;border-radius:8px;padding:14px}
.topbar{background:linear-gradient(135deg,#0B3D6B,#0D2D50);border-radius:8px;padding:12px 16px;margin-bottom:12px;display:flex;align-items:center;justify-content:space-between;flex-wrap:wrap;gap:8px;border:1px solid rgba(55,138,221,.3)}
.tb-left{display:flex;align-items:center;gap:12px}
.tb-logo{height:48px;border-radius:6px;background:#fff;padding:4px 8px}
.t1{color:#fff;font-size:13px;font-weight:700}
.t2{color:#85C1E9;font-size:10px;margin-top:2px}
.rbtn{background:rgba(55,138,221,.15);border:1px solid rgba(55,138,221,.4);border-radius:5px;padding:5px 12px;font-size:10px;color:#85C1E9;cursor:pointer}
.rbtn:hover{background:rgba(55,138,221,.3)}
.importz{background:#162030;border:2px dashed rgba(55,138,221,.35);border-radius:8px;padding:10px 14px;margin-bottom:12px;display:flex;align-items:center;gap:10px;flex-wrap:wrap}
.ibtn{background:#0B3D6B;border:1px solid rgba(55,138,221,.5);border-radius:5px;padding:5px 12px;font-size:10px;color:#6BB8F5;cursor:pointer}
.istat{font-size:10px;font-weight:600;padding:3px 8px;border-radius:3px;background:rgba(29,158,117,.2);color:#5FD4A8;border:1px solid rgba(29,158,117,.3)}
#file-input{display:none}
.filters{display:grid;grid-template-columns:repeat(4,1fr);gap:8px;margin-bottom:12px}
.fg label{font-size:9px;color:#85C1E9;font-weight:700;text-transform:uppercase;letter-spacing:.05em;display:block;margin-bottom:4px}
.fg select{width:100%;font-size:11px;padding:6px 8px;border:1px solid rgba(55,138,221,.3);border-radius:5px;background:#162030;color:#E2E8F0;cursor:pointer}
.kpis{display:grid;grid-template-columns:repeat(5,1fr);gap:8px}
.kpi{border-radius:5px;padding:12px 14px;position:relative;overflow:hidden;border:1px solid}
.kpi-lbl{font-size:9px;font-weight:700;text-transform:uppercase;letter-spacing:.06em;margin-bottom:6px}
.kpi-val{font-size:20px;font-weight:700;margin-bottom:3px;font-variant-numeric:tabular-nums;line-height:1.1}
.kpi-sub{font-size:9px;opacity:.8}
.kpi-bar{position:absolute;bottom:0;left:0;height:3px}
.k-b{background:#0C2A4A;border-color:rgba(55,138,221,.4)}.k-b .kpi-lbl,.k-b .kpi-sub{color:#85C1E9}.k-b .kpi-val{color:#6BB8F5}.k-b .kpi-bar{background:#378ADD}
.k-g{background:#083D2A;border-color:rgba(29,158,117,.4)}.k-g .kpi-lbl,.k-g .kpi-sub{color:#7ED4B5}.k-g .kpi-val{color:#5FD4A8}.k-g .kpi-bar{background:#1D9E75}
.k-a{background:#3A2205;border-color:rgba(239,159,39,.4)}.k-a .kpi-lbl,.k-a .kpi-sub{color:#FAC775}.k-a .kpi-val{color:#EF9F27}.k-a .kpi-bar{background:#EF9F27}
.k-p{background:#221C50;border-color:rgba(83,74,183,.4)}.k-p .kpi-lbl,.k-p .kpi-sub{color:#AFA9EC}.k-p .kpi-val{color:#9D97E8}.k-p .kpi-bar{background:#534AB7}
.k-o{background:#3A1205;border-color:rgba(216,90,48,.4)}.k-o .kpi-lbl,.k-o .kpi-sub{color:#F5C4B3}.k-o .kpi-val{color:#F0997B}.k-o .kpi-bar{background:#D85A30}
.tabs{display:flex;gap:2px;margin-bottom:12px;background:#162030;border-radius:5px;padding:4px;border:1px solid rgba(55,138,221,.15);flex-wrap:wrap}
.tab{font-size:10px;font-weight:700;padding:7px 10px;cursor:pointer;color:#85C1E9;border-radius:4px;background:transparent;border:none;white-space:nowrap}
.tab.active{background:#0B3D6B;color:#fff}
.tab:hover:not(.active){background:rgba(55,138,221,.1)}
.view{display:none}.view.active{display:block}
.g2{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:10px}
.g3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px;margin-bottom:10px}
.g13{display:grid;grid-template-columns:1.4fr 1fr;gap:10px;margin-bottom:10px}
.g31{display:grid;grid-template-columns:1fr 1.4fr;gap:10px;margin-bottom:10px}
.g6{display:grid;grid-template-columns:repeat(3,1fr);gap:8px;margin-bottom:12px}
.panel{background:#162030;border:1px solid rgba(55,138,221,.15);border-radius:8px;padding:12px 14px}
.mb10{margin-bottom:10px}
.pt{font-size:10px;font-weight:700;color:#85C1E9;text-transform:uppercase;letter-spacing:.05em;margin-bottom:10px}
.tbl{width:100%;border-collapse:collapse;font-size:11px}
.tbl th{text-align:left;color:#85C1E9;padding:6px 8px;border-bottom:1px solid rgba(55,138,221,.2);font-size:9px;text-transform:uppercase;background:#0F1923;white-space:nowrap;font-weight:700}
.tbl td{padding:5px 8px;border-bottom:1px solid rgba(55,138,221,.08);vertical-align:middle}
.tbl tr:hover td{background:rgba(55,138,221,.06)}
.tbl .r{text-align:right;font-variant-numeric:tabular-nums;font-size:10px;font-family:monospace}
.tbl .tot td{background:#0B3D6B;color:#fff;font-weight:700;border-bottom:none}
.badge{display:inline-block;font-size:8px;font-weight:700;padding:2px 5px;border-radius:3px}
.batl{background:rgba(55,138,221,.2);color:#6BB8F5;border:1px solid rgba(55,138,221,.3)}
.bgua{background:rgba(239,159,39,.2);color:#FAC775;border:1px solid rgba(239,159,39,.3)}
.bmag{background:rgba(216,90,48,.2);color:#F5C4B3;border:1px solid rgba(216,90,48,.3)}
.chip{display:inline-block;font-size:8px;padding:2px 6px;border-radius:3px;font-weight:700}
.chi{background:rgba(29,158,117,.2);color:#5FD4A8;border:1px solid rgba(29,158,117,.3)}
.chm{background:rgba(239,159,39,.2);color:#FAC775;border:1px solid rgba(239,159,39,.3)}
.chl{background:rgba(216,90,48,.2);color:#F5C4B3;border:1px solid rgba(216,90,48,.3)}
.prog-row{display:flex;align-items:center;gap:8px;margin-bottom:10px}
.prog-name{font-size:10px;font-weight:600;width:110px;flex-shrink:0;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
.prog-track{flex:1;background:#0F1923;border-radius:4px;height:10px;overflow:hidden}
.prog-fill{height:100%;border-radius:4px}
.prog-pct{font-size:10px;font-weight:700;width:42px;text-align:right;flex-shrink:0}
.prog-val{font-size:9px;color:#85C1E9;width:165px;text-align:right;flex-shrink:0;font-variant-numeric:tabular-nums}
.stat-row{display:flex;justify-content:space-between;align-items:center;padding:6px 0;border-bottom:1px solid rgba(55,138,221,.1)}
.stat-row:last-child{border-bottom:none}
.stat-lbl{font-size:10px;color:#85C1E9}
.stat-val{font-size:11px;font-weight:700;font-variant-numeric:tabular-nums}
.pos{color:#5FD4A8}.neg{color:#F5C4B3}
.scrollx{overflow-x:auto}
.sep{height:1px;background:rgba(55,138,221,.15);margin:8px 0}
.leg{display:flex;flex-wrap:wrap;gap:8px;font-size:10px;color:#85C1E9;margin-top:8px}
.litem{display:flex;align-items:center;gap:4px}
.lsq{width:10px;height:10px;border-radius:2px;flex-shrink:0}
.sem-legend{display:flex;gap:20px;flex-wrap:wrap;margin-bottom:12px;padding:10px 14px;background:#0F1923;border-radius:5px;border:1px solid rgba(55,138,221,.15);font-size:11px}
.sdot{width:13px;height:13px;border-radius:50%;flex-shrink:0;display:inline-block;vertical-align:middle;margin-right:5px}
.sg{background:#1D9E75}.sy{background:#EF9F27}.sr{background:#D85A30}
.kpc{background:#0F1923;border-radius:5px;padding:12px;border:1px solid rgba(55,138,221,.2)}
.kpc-title{font-size:9px;font-weight:700;text-transform:uppercase;letter-spacing:.05em;color:#85C1E9;margin-bottom:8px}
.kpc-val{font-size:20px;font-weight:700;line-height:1.1;font-variant-numeric:tabular-nums}
.kpc-sub{font-size:10px;color:#85C1E9;margin-top:4px}
.kpc-bar{height:4px;border-radius:2px;margin-top:8px;background:rgba(55,138,221,.15);overflow:hidden}
.kpc-fill{height:100%;border-radius:2px}
.kcg .kpc-val{color:#5FD4A8}.kcg .kpc-fill{background:#1D9E75}
.kcy .kpc-val{color:#EF9F27}.kcy .kpc-fill{background:#EF9F27}
.kcp .kpc-val{color:#9D97E8}.kcp .kpc-fill{background:#534AB7}
.kco .kpc-val{color:#F0997B}.kco .kpc-fill{background:#D85A30}
.kcb .kpc-val{color:#6BB8F5}.kcb .kpc-fill{background:#378ADD}
.total-strip{background:#0B3D6B;border-radius:5px;padding:10px 14px;margin-bottom:10px;display:grid;grid-template-columns:repeat(7,1fr);gap:8px;border:1px solid rgba(55,138,221,.4)}
.ts-item{text-align:center}
.ts-lbl{font-size:8px;color:#85C1E9;text-transform:uppercase;font-weight:700;letter-spacing:.04em}
.ts-val{font-size:12px;font-weight:700;color:#fff;font-variant-numeric:tabular-nums;margin-top:3px}
.ts-sub{font-size:9px;color:#9FE1CB;margin-top:1px}
/* Section dividers */
.sec-header{font-size:10px;font-weight:700;text-transform:uppercase;letter-spacing:.1em;padding:6px 10px;border-radius:5px;margin:14px 0 10px;display:flex;align-items:center;gap:8px}
.sec-header::before{content:'';display:block;width:3px;height:14px;border-radius:2px;flex-shrink:0}
.sec-ejec{background:rgba(55,138,221,.08);color:#6BB8F5;border:1px solid rgba(55,138,221,.2)}.sec-ejec::before{background:#378ADD}
.sec-fin{background:rgba(29,158,117,.08);color:#5FD4A8;border:1px solid rgba(29,158,117,.2)}.sec-fin::before{background:#1D9E75}
.sec-mat{background:rgba(239,159,39,.08);color:#EF9F27;border:1px solid rgba(239,159,39,.2)}.sec-mat::before{background:#EF9F27}
.sec-mo{background:rgba(83,74,183,.08);color:#9D97E8;border:1px solid rgba(83,74,183,.2)}.sec-mo::before{background:#534AB7}
</style>
</head>
<body>
<div class="wrap">

<div class="topbar">
  <div class="tb-left">
    <img class="tb-logo" src="data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/4gHYSUNDX1BST0ZJTEUAAQEAAAHIAAAAAAQwAABtbnRyUkdCIFhZWiAH4AABAAEAAAAAAABhY3NwAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAQAA9tYAAQAAAADTLQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAlkZXNjAAAA8AAAACRyWFlaAAABFAAAABRnWFlaAAABKAAAABRiWFlaAAABPAAAABR3dHB0AAABUAAAABRyVFJDAAABZAAAAChnVFJDAAABZAAAAChiVFJDAAABZAAAAChjcHJ0AAABjAAAADxtbHVjAAAAAAAAAAEAAAAMZW5VUwAAAAgAAAAcAHMAUgBHAEJYWVogAAAAAAAAb6IAADj1AAADkFhZWiAAAAAAAABimQAAt4UAABjaWFlaIAAAAAAAACSgAAAPhAAAts9YWVogAAAAAAAA9tYAAQAAAADTLXBhcmEAAAAAAAQAAAACZmYAAPKnAAANWQAAE9AAAApbAAAAAAAAAABtbHVjAAAAAAAAAAEAAAAMZW5VUwAAACAAAAAcAEcAbwBvAGcAbABlACAASQBuAGMALgAgADIAMAAxADb/2wBDAAMCAgICAgMCAgIDAwMDBAYEBAQEBAgGBgUGCQgKCgkICQkKDA8MCgsOCwkJDRENDg8QEBEQCgwSExIQEw8QEBD/2wBDAQMDAwQDBAgEBAgQCwkLEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBAQEBD/wAARCABZAOIDASIAAhEBAxEB/8QAHgAAAQMFAQEAAAAAAAAAAAAAAAcICQIDBAUGAQr/xABMEAABAwMDAQUDBAwLCAMAAAABAgMEBQYRAAcSIQgTMUFRCRQiMjZhcRUWFyM4QlJVcnSBsjNic3WCkZKTs9HSGFRYlaGxtLUlNNP/xAAcAQABBQEBAQAAAAAAAAAAAAAEAAEDBQYHAgj/xAA9EQABAwMDAQUEBwYGAwAAAAABAgMRAAQhBRIxQQYTIlFxMmGBoQcUM1KRscEVFkJyktEXNKKy4fDC0vH/2gAMAwEAAhEDEQA/AJU9Gubv66X7QoCqpFjIfeW6lltKyeIJycnHUjAOkv8Au43X+baX/duf69Y3Xu3ejdnLoWd8shcAwEk4PGfhVzp+gXupNd8wkbZjJApdNGkL+7jdf5tpf925/r0fdxuv820v+7c/16pf8W+zX31/0Gjv3Q1T7o/qFLpo0hn3cbs/NtL/ALtz/Xrz7uN1/m2l/wB25/r0v8W+zX31/wBBpfuhqn3R/UKXTRrgNtNxajeMuZAqcKOy7HbDyFscgCnOCCCT16jXf62+jazaa/ZpvrFUtqmJEHBg4NUd7ZPae8bd8QofrmjRrRX1elB25s6s33dEhTFKoUJ2dLWhPJXdoTkhI81HwA8yRpgNd9sAw3OcbtnYdyRDSoht6dcIZdWn1LaI6wk/RzVq8at3X/YE1Vv3bNsQHVRNSN6NMO2/9rXthWpTUTcbbit2ulxQSZUKUmpMtj8pQCG3MD+KhR+g6enZN92buRbsa7LEuSBXKRLH3qXDdC0ZwMpV5pUMjKVAKHmBpnWHGfbEV6Zumbj7NU1vtGjVLi0NIU44oJSgFSifAAeeoanqrRqPK8fa6Uik3ZOplo7MOVmiRH1Msz5Vd90ekpScd4GhHcCAcZAKicYzg9Ao+1ftQ9g76qEaj3lCq1jypJCEv1AJfgpWfAKfb6oH8ZaEpHmRopVk+kbimgk6jaqVtC808bRrHgT4NUhMVKmTGJcSU2l5h9hwLbdbUMpUlQ6KBByCOh1kaFo2jRo03vtEdt/Zzs4V5i0boRV6vX3o6ZS4FKYQsx2lH4C6ta0pSVYJCRk4GSACCfaG1OHagSajcdQync4YFOE0aY5Tfa07GyZKWqlYV6QmScF1LUZ3A9eIeGnNbP8AaL2a33gmVtnfEKpvto5vwF5YmsDzK2HAFgZOOQBSfInXty3daErTAqNq7YeMIUCaUnRo0ahoijWvq9fodAbZdrdXiQEyHUsM+8PJQXXFHCUIBOVKJIAAyTrPzpq9xQZXaN7Qk2j0yrzqfRNv4q22ajFVhTVRKujiD4cu9T09Uxz1GdH6fZpu1KLitqEiSfy+JOKq9U1BVihCWU7nFqCUp4nqT6ASadTo0kFF3hqFnNVG1d5GmYdwUiC9NjzW/gi1yO0gqLjBPQO4GFN+IPUdOgv9mi4r6vHbn7cL8q5myKvOfdho7lttLEZKuCUAJSMjklZBOTgp66TmnPMtKeXG0EAH70zG3zED/ppM6sw++i3QDuUCSPu7YBCvIyQBzPPGaVjRo0aAq0pPt7fmg1+vN/ur03O7rppVk2zUbrrbikQqYwX3uAypQ8AlI8ySQB9JGnGb2/M9r9eb/cXpmPaOfm1i0om19FhtPVa+5SabDW/ISwyz3ZDy1rWrp4IwE+JJ6ZPQ/OPb7TP2z24t7GJCw2DGPDJKjJ8kgn4V0ns/dfUtCcf6pKo9YEfOK1EPfnc+pxGalTOzzXXocptL0dxU9KSttQylWCjpkEHV77tW7n/DnW/+Yo/0a0todqSyKPbdPoVwUStM1KkMppspESOJLPeMDuiUOpICgeGcj18/E7n/AGtNsfzZcv8Ayw/6tVdzoF2w+tpOhAgEgHc8ZAPMhyD8KMa1BlxAUb+CR5I/9a5eh753/UbygomzoUOVKuNFDesdVPUZkeIU5VMMjxJT1J6BGOunJg50hn+1LtF759kftfrvvfDu+/8AsQO84+nLOcfRpQtud2bN3Qjy3bXmPF6ApKZUWSyWnmuWeJKT4g4OCCR0Oqjtdp10423dN6YbVttISogEgmeSYHoCZJ6kmKL0i4aSpTSroOqUZHnHl/8AMeQpe9ivnDUf1IfvjSedvHtgyOzlbMK1bDdjOX3cKC7HU80HUU6ICQqQpB6KUVApbScgkKJBCcKUPYr5xVH9SH741El2w9yJ+6PaRvq4pb5XHiVR2kwEZ+FuLFJZbA9OXArP8Zatd++hlgP9nGt3AUv/AHGuZfSDdKtr9ezkhI+VPA7G+/u43bCp+4HZ13zqZrECqW89IZq7ERqPIjAuIaKD3aUoV1cStGU5yhQJIIA1rPsgauZEgSd9IiWAo9wUUFRWU+XIF8AH6s6cL7O/YqkbU7B0i7nqcgXJfUZqszpShlwRXByisg+SQ2UrI/KcVnyw6bXS3bosuqDGBWXYskvsoNz4lfHg1Dfvx7OPe/ZukybpobsS96BDbU9JepbS0S4zaRlS3IyskpAyctqXgAkgDrpLuzV2lL57NV9s3Nbcl2TR5TiEVqjKXhmoMD6D0S6kElCx1B6HKSpJngIBGDqO7tIezCr18bpS7y2WrluUWjV133ibTJwdZTBfV/CLZDaFBTajlXD4eJJA6YwQxfJdBbuKEutMUwoO2kyOlP1si9Lf3Ds+kX1a0z3qk1uI3NiOkcSW1jICh5KHgR5EEaYxc3tYKFR90JltR9rVzbPhT1wX6kZ/GU62lfBb6GeHHHQkIKskYyUk9Hl7L7YQdl9p7c2wp9QcntW/CEZUpaOBfcJK3HOOTxBWpRCcnAIGTjOoDbt+cta/X5P+IrUVjbtPqXuyBxU+pXb9shspME8/KpLb59lHYV31qZdO3e6U2gUyrKM2LT5FNEtuOHPi4oc7xCu76/CCCQMAk+Omd9pbsY7r9mVLFXuNUKtW1MfEePWqdy7tLpBKW3m1Dk0shJI+Uk+AUTkamqs35oUP+bY3+EnTf/aOIQvsiXkVoCuL1NUnIzg+/MddK2vXu8CFGRMU93prBZU4kQQJprPsse0BcUK85XZ9rk5yXQ6jFeqFFQ6okwpLfxutt+jbiCtZT4BSMj5SsyaVWqU6h0yXWavMaiQYLC5MmQ6rihppCSpS1HyAAJP1ahe9nT+F9ZH6FT/9fI0+r2n+59Rsbs9N2pR5JYk3rUkUx9aThXuaEl15IP8AGKW0H1StQ89PeMBd0EJ/irzp9yW7JS152z+kUg15+1nvaPuU+bFsSgSrFiyi02ieh9NQmsBWC6HA4EMlQGUpLauOfiyfDrO1X2GL67S99wd/Nn65R0R7xpcCRMg1p9yOtgiOhLbiChtYKS2lHJPQhQJHLPRpXYn2CidobfOn2xXWFuW5SGF1itpSoo72O2pKUs8h1HeOLQk4IPHmQQRqb6NGjwozUOIw2wwwhLbTTaQlCEJGAlIHQAAYA16uVoslpDAgxmvFkhzUWlG5MpnHrURN1eyx7TNv0xVRpUyzrjcQnKodOqTqHz+j7wy2g/2gfo02NxrcTZm+wlxFYtK7LekhQyFxpUV0DIPkcEH6UqSfMHX0L6bV22OyRT+0rZCJtuMQol90QcqXNdPdpkNZyuK8oA/AepST8lYHgFKymNSUVbXuDTXWjpSjfbzI6Vidhrtds9pKzn6Fdao8e+7caR9kW28JTPjnCUzG0+WVfCtI6JUR4BaQFH7WNy1+zuzfuFctr1R+m1WBRHlxZbCuLjKjhPJCh1SoAnBHUHBHhprHYE7FG8Gym50/c3dRiFRkM016nQ6exNbkuyFuqQS4tTRKEoAR0GeRJHQY6uV7an4Km5v8wvfvJ0M6loXIDeRIo1hbyrMl4QoA+vrUavZY7YnaCsisyrQZueTclGqEaQpbdafclLp7hSeMhl1ZKkkLKcoJKFcj0BPIPI7JN/1yo2RVKZs/bFOr9X+yTiq7U6nVm2ERn+oQhTKeT6k8RnkQOSivHhnUc1tI+0Da6fdTiu7qdexHh/lJQchJH045r/YnWvsfcu+LQrEfcjbq45VFu2ioHvTkY/8A3Y6SPjcQcpdA6BxCgQoYVjoo62L1s2zadylI3rhRBmIHAwR6xXP2Lxx+++sLWoNtygERIJjcRIP8s1JT2oaFuyKBRW7/AL3pVTm1ephmBQ6VTg2w2viQVJdX98VgqQnr+Xp2Nj2xHsyz6NakZQUilQmYpWBjvFJSApf9JWT+3TDNoN/5faV3R2uuPdl2j257qVMsMiQW2JsxCnFoLYc+St1aGhwychGASSBqQ/VJrTjjdrb2q4BgqIAAGTjj3D51o+zrLT15dXrZJEhAKiSfCJVz5k+mMUaNGjWcrXUn+9vzPa/Xm/3F6Zh2pabAm7I3HJlxGnnYCGJEZa05Uy73yE8knyPFSh9ROnn72/NBr9ea/dXpmHamqcCDsncEKXKbafqSWYsRsn4n3e+QvgkeZ4pUfqB189dsg4fpBsu6mZZ459vPymfdXRdF2/u6/v4hf5V0Nov2tYO0tIqclMal0mBRo8p9SUYSnk0lS1YAyVKUonzJJ9TriU9rDbp1PeRrTvN9pXVDrdHBSseRB7zwOtfupWKZW+yK/PpE5qUx9iKY13jZyAtDzCFpPoQpJBB9NLPZ2E2hQ0pOAKZFAA8vvSdYd+3sbO3c1DU2VuuLfcRG/Zt2BKiT4VEklfWIir1Dj7zibe1WEpCEqnbumZHmMYpHKH2iKnW6nT6szbNLatapXCi2mWnZ2KyiQsAh5cbwDfXBAJI9fDOXYwCO1BuClACQaVBJA6Ang310pg27sVF0KvVFq0wVxRKjPEdPfciMFWfysfjeP06TOyfwodwf5qg/uN6PF/pN8xdnSbcsgW0KBVulXetZ5P44nyFDli8YcZF24Fku4gRA2K/7GY86dzsV84aj+pD98ahc3kpUqjbtXvRpqSmRDuGox3AfEKTJcB/7amj2K+cVR/Uh++NMB9p5sJPsXdwbw0emqFvXsE+9Otp+CPU20BK0qx8nvEIDgz8pXe+mu8/Qo4E9nGknqV/7jXMfpHaK79Sx02/MCpIOzVdFMvHs/bd3BSVoLD9twG1JR4NutMpbdb/ouIWn+jpStRJdgztwQdikObWbpvSFWXMfVIgz22y6ukvrxzCkj4lMLPxEJBKVZIBCjiU219wbEvaks120Lxo1Zp8hIW3IhTW3kEYz1KScH1B6jz1v7q3WysyMdKprK7RctCDkciug0aRLfjtf7J7BUeQ/cN1RKpXA2oxaDTX0PTHl4+EKCSQykn8deB445EY1ElfPax3/ANwNzHtxmdwa9Sqg5K7ynQKXNdRGhpyO7ZaZB4qAAAPIErOSrOdereycfE8CvF3qTVqQnk+QqdhfyD9WvnWu75y1r9fk/wCIrX0GWJOuOqWHb1SvGCmFX5dJiP1SMlOAxLUykvIx5cVlQx5Y18+V3fOSt4/36T/iK0ZpQhSx6frVfrZlLZ9f0r6FLN+aFD/m2N/hJ0gHtGvwQ70/lKb/AOcxpf7O+aND/m2N/hJ0gPtGfwRL0/lKb/5zGq5j7dPqPzq3uf8ALL/lP5VHV7On8L6yP0Kn/wCvkadF7XyJKXae205BV7szUai04PLmtpko/wCiF6a77On8L6yP0Kn/AOvkakm7deyMvfHs+VikUOOt6v0FxNcpTSE5U86ylQWyB4kraU4lIH4/DVncrDd4hR8v71S2bZd09xCeZ/KDTQPZEVamMbj7gUR5aBUJlEiSY4PiWmn1Jdx+15rP7NSia+f7Y3d+4dh90aLubbjSXpNJdIfiuKKESo6xxdZUR4ckk4ODhQScHGputku0Bthv9a7Ny7e3ExJXxHvdOdWETILmMlDrWcj6FDKVYyknUGpMqDnejg0Vo9whTXck5FKPo1bffYjMrkSXkNNNpKlrWoJSkDxJJ6Aaj17bvtCmqQhW2HZzuxtyopcKavckLi42wEn+AiudUqWT8pxOQkDCSSSUhMsLfVtRVjcXLdqjes/81IdpHu12zAm9nO9qPUJiIyKpAEFBJ6qW44kBKfUnr/UT4A6bx7MvtD7t7vx7xtLcqrzLhj2+iJKhVeUAp5svFwKjuOY+PPDkknKhhQyRgDN7dm6zLlVYsaO6r7H24wanVFISVffijIyB5NtEqP8AKH01aaXpqn9QSwvhPiUfcM/8fGqXWtXTbaWq5bHiV4UjruOPlz8Kj33Rh1y7rgj2xalEkPwKG0I4LSMNB0gZHI/COICU+PkdYlB2wNCq0F247yg0ycXUBqJGUHpClKOAgjw65weigQfMa1V+3huCxWZVGqtecbbbOWxD+8tONK6pWnj1IUDnqTrqtmtpbmfjwt2atB93oPvbsaA6/kLnSEo+NTQ/GQ3yTyX4BSkgZOcbIrZfvY2kqKozgCPcM4A8+lc/Db9vp+7eAhKZwJJnzJxkny606XYbsp1veW9rXrUjvKNYVkympq3mxhc6U0tJais+gSEZWvyCwBlR+GTTXAbD2cqxdprboL6OMr3NMqUMdQ88S4tJ/RK+P9HXf6xOt3pvr1ax7IMD0GBXRuzunDTdObbPtEAq9Tk/hNGjRo1U1eUn+9vzPa/Xm/3F6atuNYtVut+g122rhRRa9bM1U2nSnYqZLXJaChaVtqOCCk9D4gjpp6N1WzBu2krpM9bjaCtLiFtkckqHgev1kft1xH3CaN4fZyd/YR/lri/bPsp2iu+0SNZ0UCUpABJTgiQQQrBBB94g1ttE1bTWdOVZX05JxB4xGR6U1KjbLUiPtfP20r9SeqTdYW/JqEtDaWFLkOud4pbaBlKAFgFI6j4R9WuTjbB7qQI7UGndpS4GYsdCWmGjTkq4NpGEpz33XAAGns/cJo/58nf2Ef5aPuE0f8+Tv7CP8tZprsp29aU4uEK7xRWrd3ShuPJAUCAT7o4HkKs1at2fWEiSNogRvGB0wRPxplX3Dt4P+Jqv/wDK0/8A7a6va/aFO30+q3DVrqqFy1+s92mXUpiQgltAwlCUAnA8PEnwHhjGnVfcJo/58nf2Ef5a8+4RRvz5O/sI/wAteLvsh26vGFWziGwhWDtDKJAIMEoSkxIBiYxTs6xoLDgdSVSOJ3mOnBJFaPYr5w1H9SH740o+423Nn7sWbUrCvujtVKjVRvu3mV9FJIOUuIUOqFpICkqHUEDVmzNvaXZbsiTElPyXpKQhS3cDikdcAD6f+w11euv9gdGu+z2iNWV4AHAVEwZiVEjNY3tDeM6lfLeZykgDI90cVDr2ifZ0bybR1CTVtv6dKvm1FLUpl6A1znxkeIS/HT1UQOnNsFJxkhGQNNUmMVKgzHYFQYlU6U2Sl1l9KmXEn0UlWCP26+jXWJMpNKqJSqoU2LKKfkl5lK8fVka6K3qi0iFiaxj2itrVLao93NfPxYe1G5m6M5MHb2xa3cDziwkqhRFrbST+W7jggfSpQGpK+xx7OuNtTVYW6G9bkKqXREKX6ZSGFd7FpjviHXF+DzwPhgcEEZBUeKkvkaaaYbSyy2ltCBhKUgAAfQBqvUb+ouPDakQKmtdJaYVvWdx+VeKGUkeo18/F9bdXtC3crG2z9s1D7ZXau9FapwYUXnVrcPDgnGVJUCCFDoQc+GvoI1ZMOIqUmcqKyZCElCXigcwn0CvHH0aitbo2pOJmpr6xF6EyYisS3Ib9Ot6l0+SAHosJhlwA5wpKAD/1GkO7etr167+yre1ItulyKjOS3ElCPHbK3FNsymnHClI6nCEqOB5A6cFo0OhZQsLHQzRbjYcbLfmIqGn2alsV6tdqigV2mUx9+n0CNPfqMlKCW46XIjrSApXgCpbiQB4nr6HUy2rMaHEhhYiRWWA4suL7tATyUfFRx4n6dXtTXVx9ZXviKHsrT6m33czmajy7a3s7qjdVYqO7uwcFpdQmqXKrFuBQb94dJyt+KTgc1dSpskZOSk5PExzzoV4beXCuDUI1YtquQlfE24l2HKZP1HitP16+iXXPXfYFhX5GRDvqzqHX2G8htFTgNSQjP5PeJOP2aJY1FTadjgkUHdaQh5W9s7T8qgFr25e41zQxBufcK5qvFSMBmoVeRIbA/RcWRpSNgOyHvN2hanGFsW6/TbfWcyLgqLSmoTbeepbJ6vK9Et56+JSMkTF0ns29n6hzEVCk7K2VGktnkh1NEjlSD6pJR0P1aUZCENoS22kJSkYAAwAPQalXqkCGkxULeiyqXlz6f3pG9vdtdtux1sfLgUBsmLSmFzZ817HvFTmlISFLx4FauCEpHRIIHqS12kbYXhuvslvTuV9jXqrXa5SpkKmMoTydkSFEOvltPrgJQkDxypI8MaVftnXtPrVWoGy1uffZM59qVLbQcqW6tXCO1/WSoj9A6cXttZMLbqx6PZ0HCk06MlDrgH8K8ficc/pLKj9GceWrALOm6Z3qvtHz/oT/AHP4iqstp1jWe5T9jbD/AFqH/iPwPrUR+z3Z9q1z063Lm7QFjXJRrLolbapkmc5HXGdfjLBPdKSoBwNpWAC4keBKUnlp3+5dNoW4faGs7Z+z4sVi2rZaiwEMQwBHaYSkPvBvj0ADQSj606druJTLcrFi12BdqAqjrgPLmHOChtKSorB8lJ48gfIgaa92LNr7hj3NP3FuGiTYURqD7vTly2VNl9bqvicRyAJCUoIz4Hn08Do2xv0OW7moOYcbSUjyJVhJ9RkH3RVdqWluNXTOlNeJp1QWrzASZUP5SYI98inhJASkJSAABgAeWvdGjWLrodGjRo0qVGuduepVlNRplv0GTHiyqkH3TKfZLyWm2gnOEBSeRJWkeIAGT9Gui1yV1TYlIuu3axU30x4TbU2Ot9fRCHFhsoCj5ZDaup9NAam53dvu3QJSCZiAVAHPTE56c0RbJ3ORE4P4wY+da2JcV4VqU1bcWTAgVGP70ZkxcVTrawy6ltJbb5JPxcsnKumOmdeQLkvG51Jg0iRTadJgxVPTFusKfQ66JDzPBA5J4pJjrPI5IBT8J66x4N2xV3Szc1ZeZh0yTGmw4MpQKW3kofQUnJ81JBI8M46a922yqrVJ/ioIk09Elrkkgqacnz1oVg+qVJP7dZpm5L9y2wl5SgokHxEHaEpKTgyJyZEbpMkirJbYQ0pZQAREY6kkH19OlVRbtu25Yr1SoDlPhN06AxLeYfYW8ZLq2ysthQUOCQBgKwo9fDRKvG6ZkCpXXTFQo9MoyW1OQX2FKek5YbeWO8CgGyEugD4VZIOceOuUp4tB23wm6IUZiczR2F014FxD0gFCvk8T8akr6AAZGtgupJp9o3RblakKRXailotRnMl6QtyFHbBSPxsuIWOnmDnQKdReUzuceyUkkhR9oBZSCIG0yBCRhcTnrObZAXCUYkDjpInOZ9eRNdBJuy5kok3O09CFHi1L3D3AsKL7yQ6GisOcsBXIkhPEjA8dW03bdfu0e6C5CXSZlRVT0QUR1d80nvVMpdLvLBPJOSnjjHmNaF636TDt2o3k3CQmswK84puRknBEsIwR4EcSR4a2NJudNHtuNbEIsu1n7KPxpMJYUXGmVSXFLcIGMANnkFHp9ep2rx/vQLl0oBQFiFEyonGMZOR3YlOJEniNbDeyWkyQqDiMRnz4x4uaqp95XnWaJIrkGTTWG6NT2ZUpp2MpZmOKa71YBCh3Qx0HRXXXXV653KdZqrmhRkrccjtOstunACnOITyx5AqGcemk0tqrU+kWdW6bUpIYlVOjxzCaUDyk8ovdjux+MeYIwNdnd8d6Jta3EkIKHWY8JtaT5KC2wR/XqXTb99dk673hKw2onMwoFUY6YAx1iffXm5t20voTtgbgPUQJ9c/hxWHUbsuy256raqMmn1CozURlQZSI6mW21PPhkhxHJRISSCCCM69k3VdlNqK7PkSqfJqj0mM1HqAjKQ0lt1K1KUpnmcqT3ZAAXg5B6Y663cbLd+wZyge4gRIUyQoAnu2W6ghS1kDrgAZP0DWFX0Ue8L5Yeb7uoUl+dBiLcQT3bi0tPqKQoeJGUk4PTI0NdXtwy+phtwyFhIBUcpO+c5PMDdkpgQfORpltbYWpIykkmOoiP1xwa3ybuutyqix0yqf9lvfVxzUxGUWe6SwHiruefy8KCccsA566ti5b9Zp9WrUibSFMW4+4xJjpirBmBvBWsL5/ejxIIThXXpnWqo8KLRd04tu01oNQIM+SthsdeJdgNrX1PU9fXWzlfM3cTP8Avk7/AAk69tv3Ljbi1uKCkKcThRgbEbgOm6FfxESoe15Uym2kqSEpEKCTx5qg+kjoMDp51mrui6F99cjL8EUePVhTDBUwovKR7wGC73vLAPI548cY889NdBaFYm1m1ItXmlBkPNrUopThOQpQHT9g0nSbYoKrdnXK5T0GpIuYgP8AJWR/8mlPhnHyTjw1ubbudql2/SbWiracrAlqhyoagS402FrLiyB4AJGQo9D9OirDUXmrhJulwlTe72iZUpQAgECCYwkSBmOtRP2yFNkNDIVHEQAPy95+NUTa1fgtSmXRDuWnpcqjEIR4BpXNS5DyEApDnejoVFSvk9B064650y5rrbbqNwsSIApdImmG7DVHUXXwhSUOOBzlhJyVFKeJGAMnr00dq3FQ1O2zFrFcgQo1vUOK9wkSEtlcp5gAEBR68Gievl3g9elmp2xb0y27quR6ntuT2qvJLcjkegD4wcA4PQ+mhBePPNF63cJO0yN55Qkkq6x4iRtgJO0dKm7lCFhDiYz90cE4HTpmckTXTtXDdji2rhD0FVIdqv2MEFMdXfJQZHu4e73ljPL4injjj+N5a0aKtc96UyPUWZFOa+wEaLVXW3mFKEuSWlOBPRQ7tKRgg4V8XXHTrs6LdMej09q3IzjTlZVXHY7kJYJcS05MUpa8DyDKisK8Og8fDXP2jWqXQLdqLVXmJjLqFGiORErBy+BHLZCPyjyGMDrr07dpWWkLfO1SSV+LAVtnmceKPDiOIhUV5S0RvUlGQRtxyJjjrjr1+Fb6ReVzy6dUrspLkFil0ZtpxyG8wpbskGO2+v74FAN4S6APhVkjrjx11l1VeZSaL7zTm2lypD8eIx3ueAcedS2lSsdcArycemuBiR3om2N6RJKCh5hjunEnxSpNMjAj+sa7G+1Bm3WZjgPcw58CW+oJJ4NNyWlrUQPIJSSfoGrG2uX/AKs+4tZ3bN3odzgx5YAwMY85od1pvvUJSBG6PUQn8eTSffanBoF4zJ0i36HULvqMyIti4H4a1KQXu8BIQtaygtpZICUKAxx8PDXSm6LtRUftKMuAqrmalhNR91UGu5Uwt7n3PPPIBCk45YPTqPLEuasU29arBo7aY0+iN1KClTzZVhx1SXytHIHBwEtnp1HLx1pV2lbqdxftaFMQKaqc0osclYJ9wfVnOc+Iz46Cur+7ccT3LpWjvA2CVq9kz4Rg46Bc7oGKkt7S3ZSqWwk7SogJHOMnjJ5IiPOs+r37dMZMikl6CqVEdkQ3ZAjEtPLQqPxcDZV06PkFHI9R462s66rsoE122ZsuBUahIMQRJiYqmW2+/e7rDjfNXhjIwrr19OvB3DEhQHqhQG0IRTafJlstNnwQypUNakk+YytZyfX6BrZVenWqmdLbtxlh+2EPU5+qOMKLjSVpfIUeYyThs5OD06Hpqq/ad6HHU95lMCN5x4VzAjIBGVnIjdHIo36qztSdvOeBnIjPTn2eOlKVbFRrhqVToFfeYlP08MOomMMFlDyHQrpwKlYKSgg4Uc5Hhro9cjYsylrlVSl21HjihwSyIz7JUoOPLClOjkSQrHweH5Xnrrtb3TVhy2CgrdlWZn+I4k5IHAV1AnrVBcja6REce7oOnSeY6cUaNGjR9QUaodZZfbU0+0hxCuikrSCD9YOq9GlzSq27GjvN9y8w2430+BSQR08Oh16Gmg4p0Np5qSEqVjqQM4BPp1P9Z1Xo00ClVn3OIA0kRWcMHLQ4D73+j6fs1UphhbiHlsoU43ngspBKc+OD5auaNKBSmrRjRy2pox2yhSuRTwGCc5yR6566993j96X+4b71SeBXxHIp9M+mrmjSgUpqyIkQBoCK0Ax/BfAPvfl8Pp+zVbrLL6O7eaQ4g4PFSQR0OR0P06r0aUClNUFhku9+WUd5x4c+I5cc5xn0z5aoREiNobbbispQ0eTaQgAIPqB5eJ/r1e0aUClNWvdIvfCT7s13wOe84DlnGPHx8On1aDFjFDrZjtFD5JdTwGFkjB5Dz6eurujSgUpq17tG4Fr3dvgVcyngMFWc5x656/Xr0R44dU+GGw4tISpfEciPQn01c0aUClNYS6JRnVcnKRCWcBOVR0E4AwB4eQAGsj3aN3amvd2+CzlSeAwT6kau6NMEJHAp5Jq33DHfGR3LfelPAr4jlx9M+OPo1T7pEw0n3VnDBy0OA+A/xfT9mr2jTwKaatKjRlIdbVHaKX896koGF9MfF69AB11cwPTXujTxSqyiJFbQhpuM0lDauSEpQAEn1A8j1Ovfdo/e9/7u33mc8+A5Zxjx+okau6NNtHlTyax3afAeKi9Bjuc88uTSTyzjOcjr8kf1D01WxFjRmu4jR2mmuvwIQEp6/QNXdGltEzFKTxVDLLMdtLLDSG20/JShIAH1Aar0aNPxTUaNGjSpV//Z" alt="CNC">
    <div>
      <div class="t1">Dashboard Financiero PRONEs 2022 - Consorcio Normalizacion Caribe</div>
      <div class="t2">22 contratos — 32 proyectos</div>
    </div>
  </div>
  <div style="display:flex;align-items:center;gap:8px">
    <span id="fstatus" style="color:#9FE1CB;font-size:10px">32 proyectos</span>
    <button class="rbtn" onclick="resetAll()">Limpiar filtros</button>
  </div>
</div>

<div class="importz">
  <span style="font-size:10px;color:#85C1E9;font-weight:700;text-transform:uppercase;white-space:nowrap">Importar Excel</span>
  <span style="font-size:10px;color:#5F8FAA;flex:1">Columnas: CONTRATO, DEPARTAMENTO, MUNICIPIO, PROYECTO, PRESUPUESTO REPLANTEO, VALOR EJECUTADO, VALOR FACTURADO POR CONTRATO, VALOR RECIBIDOS POR LO FACTURADO, VALOR ANTICIPO RECIBIDO, VALOR TOTAL RECIBIDO</span>
  <input type="file" id="file-input" accept=".xlsx,.xls" onchange="importExcel(event)">
  <button class="ibtn" onclick="document.getElementById('file-input').click()">Seleccionar archivo</button>
  <span id="import-status" class="istat">Datos cargados - 32 proyectos verificados</span>
</div>

<div class="filters">
  <div class="fg"><label>Departamento</label><select id="f0" onchange="cascade()"><option value="">Todos</option></select></div>
  <div class="fg"><label>Municipio</label><select id="f1" onchange="cascade()"><option value="">Todos</option></select></div>
  <div class="fg"><label>Contrato</label><select id="f2" onchange="cascade()"><option value="">Todos</option></select></div>
  <div class="fg"><label>Proyecto</label><select id="f3" onchange="cascade()"><option value="">Todos</option></select></div>
</div>

<div class="tabs">
  <button class="tab active" onclick="showTab(0)">Resumen</button>
  <button class="tab" onclick="showTab(1)">Ejecucion</button>
  <button class="tab" onclick="showTab(2)">Recaudo</button>
  <button class="tab" onclick="showTab(3)">Semaforo Pago vs Gasto</button>
  <button class="tab" onclick="showTab(4)">Control Materiales</button>
  <button class="tab" onclick="showTab(5)">Mano de Obra</button>
  <button class="tab" onclick="showTab(6)">Proyectos</button>
  <button class="tab" onclick="showTab(7)">Municipios</button>
</div>

<!-- TAB 0 RESUMEN -->
<div class="view active" id="v0">

  <!-- ══ BLOQUE 1: EJECUCION ══ -->
  <div class="sec-header sec-ejec">Ejecucion de Obra</div>
  <!-- Fila KPIs ejecucion: 5 tarjetas -->
  <div class="kpis" id="kpis-ejec-top" style="margin-bottom:10px"></div>
  <div style="display:none" id="fin-cards"></div>

  <!-- ══ BLOQUE 2: FINANCIERO / RECAUDO ══ -->
  <div class="sec-header sec-fin">Avance Financiero y Recaudo</div>
  <!-- Fila KPIs financiero -->
  <div id="fin-kpi-strip" style="display:grid;grid-template-columns:repeat(4,1fr);gap:8px;margin-bottom:10px"></div>
  <!-- Fila charts financiero: tortas lado a lado (leyenda al costado) -->
  <div class="g2" style="margin-bottom:10px">
    <div class="panel" style="display:flex;flex-direction:column">
      <div class="pt" style="text-align:center">Ejecutado</div>
      <div style="display:flex;align-items:center;flex:1;gap:12px">
        <div style="position:relative;flex:0 0 auto;width:260px;height:260px"><canvas id="pie-ejec"></canvas></div>
        <div id="pie-ejec-leg" class="leg" style="flex-direction:column;gap:6px;flex:1"></div>
      </div>
    </div>
    <div class="panel" style="display:flex;flex-direction:column">
      <div class="pt" style="text-align:center">Recaudo</div>
      <div style="display:flex;align-items:center;flex:1;gap:12px">
        <div style="position:relative;flex:0 0 auto;width:260px;height:260px"><canvas id="pie-recaudo"></canvas></div>
        <div id="pie-recaudo-leg" class="leg" style="flex-direction:column;gap:6px;flex:1"></div>
      </div>
    </div>
  </div>

  <!-- ══ BLOQUE 3: AVANCE POR DEPARTAMENTO ══ -->
  <!-- Fila charts ejecucion: barras horizontales + torta costos por dpto -->
  <div class="g2" style="margin-bottom:10px">
    <div class="panel">
      <div class="pt">Avance por departamento</div>
      <div style="position:relative;height:240px"><canvas id="dept-prog-bar"></canvas></div>
    </div>
    <div class="panel">
      <div class="pt" style="text-align:center">Control Costos por Dpto. Presupuesto vs Real</div>
      <div style="position:relative;height:240px"><canvas id="bar-dept"></canvas></div>
    </div>
  </div>

  <!-- Nueva torta: peso % de cada departamento en costos -->
  <div class="panel" style="display:flex;flex-direction:column;margin-bottom:10px">
    <div class="pt" style="text-align:center">Peso % por departamento en costos (Ejecutado)</div>
    <div style="display:flex;align-items:center;justify-content:center;flex:1;gap:20px;padding:8px 0">
      <div style="position:relative;width:220px;height:220px"><canvas id="pie-costos-dpto"></canvas></div>
      <div id="pie-costos-dpto-leg" class="leg" style="flex-direction:column;gap:10px"></div>
    </div>
  </div>

  <!-- ══ BLOQUE 4: CONTROL MATERIALES ══ -->
  <div class="sec-header sec-mat">Control Materiales</div>
  <!-- Fila KPIs materiales: 5 tarjetas -->
  <div style="display:grid;grid-template-columns:repeat(5,1fr);gap:8px;margin-bottom:10px" id="res-comp-kpis"></div>
  <!-- Solo gráfico de barras con 3 barras por proveedor -->
  <div class="panel" style="margin-bottom:10px">
    <div class="pt">Presupuesto Inicial vs Presupuesto Actual vs % Avance por proveedor</div>
    <div style="position:relative;height:260px"><canvas id="res-comp-bar"></canvas></div>
  </div>

  <!-- ══ BLOQUE 5: MANO DE OBRA Y ADMINISTRACION ══ -->
  <div class="sec-header sec-mo">Mano de Obra y Administracion</div>
  <!-- Fila KPIs MO -->
  <div style="display:grid;grid-template-columns:repeat(4,1fr);gap:8px;margin-bottom:10px" id="res-mo-kpis"></div>
  <!-- Grafico Mano de Obra -->
  <div class="panel" style="margin-bottom:10px">
    <div class="pt">Mano de Obra — Presupuesto Inicial MO vs Presupuesto Actual MO vs Porcentaje de Avance</div>
    <div style="position:relative;height:220px"><canvas id="res-mo-bar"></canvas></div>
  </div>
  <!-- Grafico Administracion, Adm Socios, Contingencia -->
  <div class="g2" style="margin-bottom:10px">
    <div class="panel">
      <div class="pt">Administracion — Presupuesto Inicial vs Presupuesto Actual vs % Avance</div>
      <div style="position:relative;height:200px"><canvas id="res-adm-bar"></canvas></div>
    </div>
    <div class="panel">
      <div class="pt">Administracion Socios — Presupuesto Inicial vs Presupuesto Actual vs % Avance</div>
      <div style="position:relative;height:200px"><canvas id="res-adms-bar"></canvas></div>
    </div>
  </div>
  <div class="panel" style="margin-bottom:10px">
    <div class="pt">Contingencia Total — Presupuesto Inicial vs Presupuesto Actual vs % Avance</div>
    <div style="position:relative;height:200px"><canvas id="res-ctg-bar"></canvas></div>
  </div>

  <!-- hidden placeholders -->
  <div style="display:none"><canvas id="pie-rec"></canvas><div id="pie-rec-leg"></div><div id="kpi-stats"></div></div>
</div>

<!-- TAB 1 EJECUCION -->
<div class="view" id="v1">
  <div class="panel mb10">
    <div class="pt">Ejecutado vs Presupuesto por proyecto (barras apiladas)</div>
    <div id="execbar-wrap" style="position:relative"><canvas id="exec-bar"></canvas></div>
    <div class="leg" style="margin-top:8px">
      <span class="litem"><span class="lsq" style="background:#378ADD"></span>Ejecutado</span>
      <span class="litem"><span class="lsq" style="background:rgba(55,138,221,.2)"></span>Pendiente</span>
    </div>
  </div>
  <div class="g2">
    <div class="panel">
      <div class="pt">Porcentaje de ejecucion - semaforo por proyecto</div>
      <div style="position:relative;height:300px"><canvas id="pct-bar"></canvas></div>
      <div class="leg" style="margin-top:6px">
        <span class="litem"><span class="lsq" style="background:#1D9E75"></span>Alto mayor 38%</span>
        <span class="litem"><span class="lsq" style="background:#EF9F27"></span>Medio 30-38%</span>
        <span class="litem"><span class="lsq" style="background:#D85A30"></span>Bajo menor 30%</span>
      </div>
    </div>
    <div class="panel">
      <div class="pt">Total ejecutado vs pendiente</div>
      <div style="position:relative;height:200px"><canvas id="exec-donut"></canvas></div>
      <div id="donut-leg" class="leg" style="justify-content:center;margin-top:8px"></div>
      <div class="sep"></div>
      <div id="ejec-totals"></div>
    </div>
  </div>
</div>

<!-- TAB 2 RECAUDO -->
<div class="view" id="v2">
  <div class="panel mb10">
    <div class="pt">Facturado, Recibido por Factura y Anticipos - por contrato</div>
    <div style="position:relative;height:240px"><canvas id="rec-bar"></canvas></div>
  </div>
  <div class="g13">
    <div class="panel"><div class="pt">Brecha: Ejecutado vs Facturado</div><div style="position:relative;height:240px"><canvas id="brecha-bar"></canvas></div></div>
    <div class="panel">
      <div class="pt">Detalle recaudo por contrato</div>
      <div style="max-height:260px;overflow-y:auto">
        <table class="tbl">
          <thead><tr><th>Contrato</th><th class="r">Facturado</th><th class="r">Rec.Factura</th><th class="r">Anticipo</th><th class="r">Total Rec.</th></tr></thead>
          <tbody id="rec-tbody"></tbody>
          <tfoot><tr class="tot" id="rec-tfoot"></tr></tfoot>
        </table>
      </div>
    </div>
  </div>
</div>

<!-- TAB 3 SEMAFORO -->
<div class="view" id="v3">
  <div class="sem-legend">
    <div><span class="sdot sg"></span><strong>Verde</strong> - Ejecutado menor al 80% del Total a Recibir (margen amplio)</div>
    <div><span class="sdot sy"></span><strong>Amarillo</strong> - Ejecutado entre 80% y 100% del Total a Recibir (atencion)</div>
    <div><span class="sdot sr"></span><strong>Rojo</strong> - Ejecutado mayor al Total a Recibir (riesgo de sobregiro)</div>
  </div>
  <div class="g2 mb10">
    <div class="panel">
      <div class="pt">Distribucion semaforo - proyectos</div>
      <div style="position:relative;height:200px"><canvas id="sem-donut"></canvas></div>
      <div id="sem-donut-leg" class="leg" style="justify-content:center;margin-top:8px"></div>
    </div>
    <div class="panel">
      <div class="pt">Total Recibido vs Ejecutado - contratos con recaudo</div>
      <div style="position:relative;height:200px"><canvas id="sem-bar"></canvas></div>
    </div>
  </div>
  <div class="panel">
    <div class="pt">Cuanto van a pagar vs cuanto hemos gastado - todos los proyectos</div>
    <div class="scrollx">
      <table class="tbl" style="min-width:920px">
        <thead><tr>
          <th>Estado</th><th>Proyecto</th><th>Dpto</th><th>Contrato</th>
          <th class="r">Total a Recibir</th>
          <th class="r">Ya Ejecutado</th>
          <th class="r">Diferencia</th>
          <th class="r">Ejec/Recibido</th>
          <th class="r">Avance Obra</th>
        </tr></thead>
        <tbody id="sem-tbody"></tbody>
        <tfoot><tr class="tot" id="sem-tfoot"></tr></tfoot>
      </table>
    </div>
  </div>
</div>

<!-- TAB 4 COMPRAS -->
<div class="view" id="v4">
  <div class="g6" id="compras-kpi-grid"></div>
  <div class="g2 mb10">
    <div class="panel">
      <div class="pt">Anticipo Proveedor vs Contratista - por contrato</div>
      <div style="position:relative;height:220px"><canvas id="compras-bar"></canvas></div>
    </div>
    <div class="panel">
      <div class="pt">Distribucion anticipo total</div>
      <div style="position:relative;height:200px"><canvas id="compras-donut"></canvas></div>
      <div id="compras-donut-leg" class="leg" style="justify-content:center;margin-top:8px"></div>
    </div>
  </div>
  <div class="g2">
    <div class="panel">
      <div class="pt">Porcentaje anticipo a proveedor por contrato</div>
      <div style="position:relative;height:200px"><canvas id="compras-pct-bar"></canvas></div>
    </div>
    <div class="panel">
      <div class="pt">Detalle compras y variaciones por contrato</div>
      <div style="max-height:220px;overflow-y:auto">
        <table class="tbl">
          <thead><tr>
            <th>Contrato</th><th class="r">Anticipo Total</th>
            <th class="r">A Proveedor</th><th class="r">% Prov</th>
            <th class="r">A Contratista</th><th class="r">% Cont</th>
            <th class="r">Variacion</th>
          </tr></thead>
          <tbody id="compras-tbody"></tbody>
          <tfoot><tr class="tot" id="compras-tfoot"></tr></tfoot>
        </table>
      </div>
    </div>
  </div>
</div>

<!-- TAB 5 MANO DE OBRA -->
<div class="view" id="v5">
  <div class="g6" id="mo-kpi-grid"></div>
  <div class="g2 mb10">
    <div class="panel">
      <div class="pt">Replanteo vs Ajuste MO vs Ejecutado - por contrato</div>
      <div style="position:relative;height:220px"><canvas id="mo-bar"></canvas></div>
    </div>
    <div class="panel">
      <div class="pt">Porcentaje MO sobre ejecutado por contrato</div>
      <div style="position:relative;height:220px"><canvas id="mo-pct-bar"></canvas></div>
    </div>
  </div>
  <div class="panel mb10">
    <div class="pt">Costo MO vs Avance de Obra - detalle por contrato (datos verificados)</div>
    <div class="scrollx">
      <table class="tbl" style="min-width:980px">
        <thead><tr>
          <th>Contrato</th><th>Municipio</th>
          <th class="r">Presup Replanteo</th>
          <th class="r">Ajuste MO</th>
          <th class="r">Ajuste Materiales</th>
          <th class="r">Total Ajuste</th>
          <th class="r">Valor Ejecutado</th>
          <th class="r">MO / Ejecutado</th>
          <th class="r">Avance Obra</th>
          <th>Estado</th>
        </tr></thead>
        <tbody id="mo-tbody"></tbody>
        <tfoot><tr class="tot" id="mo-tfoot"></tr></tfoot>
      </table>
    </div>
  </div>
  <div class="g2">
    <div class="panel">
      <div class="pt">Ajuste MO vs Materiales - total</div>
      <div style="position:relative;height:180px"><canvas id="mo-donut"></canvas></div>
      <div id="mo-donut-leg" class="leg" style="justify-content:center;margin-top:8px"></div>
    </div>
    <div class="panel">
      <div class="pt">Dispersion: Avance de Obra vs Ajuste MO</div>
      <div style="position:relative;height:180px"><canvas id="mo-scatter"></canvas></div>
    </div>
  </div>
</div>

<!-- TAB 6 PROYECTOS -->
<div class="view" id="v6">
  <div class="panel">
    <div class="pt" style="display:flex;justify-content:space-between">
      <span>Tabla completa de proyectos</span>
      <span id="tbl-count" style="font-weight:400;font-size:10px"></span>
    </div>
    <div class="scrollx">
      <table class="tbl" style="min-width:1020px">
        <thead><tr>
          <th>Proyecto</th><th>Dpto</th><th>Municipio</th><th>Contrato</th>
          <th class="r">Presupuesto</th><th class="r">Ejecutado</th>
          <th class="r">Pendiente</th><th class="r">% Ejec</th>
          <th class="r">Facturado</th><th class="r">Anticipo</th>
          <th class="r">Total Rec</th><th>Estado</th>
        </tr></thead>
        <tbody id="full-tbody"></tbody>
        <tfoot><tr class="tot" id="full-tfoot"></tr></tfoot>
      </table>
    </div>
  </div>
</div>

<!-- TAB 7 MUNICIPIOS -->
<div class="view" id="v7">
  <div class="g31 mb10">
    <div class="panel"><div class="pt">Ejecutado vs Presupuesto por municipio</div><div id="muni-bar-wrap" style="position:relative"><canvas id="muni-bar"></canvas></div></div>
    <div class="panel">
      <div class="pt">Detalle por municipio</div>
      <div style="max-height:320px;overflow-y:auto">
        <table class="tbl">
          <thead><tr><th>Municipio</th><th>Dpto</th><th class="r">Presupuesto</th><th class="r">Ejecutado</th><th class="r">% Ejec</th><th style="text-align:center">Proy</th></tr></thead>
          <tbody id="muni-tbody"></tbody>
          <tfoot><tr class="tot" id="muni-tfoot"></tr></tfoot>
        </table>
      </div>
    </div>
  </div>
  <div class="panel"><div class="pt">Recaudo total por municipio</div><div style="position:relative;height:180px"><canvas id="muni-rec"></canvas></div></div>
</div>

</div>
<script src="https://cdnjs.cloudflare.com/ajax/libs/Chart.js/4.4.1/chart.umd.js"></script>
<script src="https://cdn.jsdelivr.net/npm/chartjs-plugin-datalabels@2.2.0/dist/chartjs-plugin-datalabels.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js"></script>
<script>
if(typeof ChartDataLabels !== "undefined"){Chart.register(ChartDataLabels);}
// Disable datalabels globally by default — enable per-chart only where needed
if(typeof Chart !== 'undefined' && Chart.defaults && Chart.defaults.plugins){
  Chart.defaults.plugins.datalabels = {display:false};
}

// Center total label plugin for donuts
var centerLabelPlugin = {
  id: 'centerLabel',
  afterDraw: function(chart) {
    if (!chart.config.options.centerText) return;
    var ctx = chart.ctx;
    var centerX = (chart.chartArea.left + chart.chartArea.right) / 2;
    var centerY = (chart.chartArea.top + chart.chartArea.bottom) / 2;
    var text = chart.config.options.centerText;
    ctx.save();
    ctx.font = 'bold 11px system-ui';
    ctx.fillStyle = '#E2E8F0';
    ctx.textAlign = 'center';
    ctx.textBaseline = 'middle';
    ctx.fillText(text, centerX, centerY);
    ctx.restore();
  }
};
if(typeof Chart !== 'undefined'){Chart.register(centerLabelPlugin);}
var PROJECTS_RAW = [{"c": "CRE01212024", "d": "MAGDALENA", "m": "CIENAGA", "p": "URB LA MILAGROSA", "pre": 1269673307.88, "eje": 478971648.68, "fac": 571404094.76, "rf": 56738743.61, "ant": 441073250.0, "tr": 497811993.61}, {"c": "CRE01372024", "d": "ATLANTICO", "m": "BARANOA", "p": "SBN 11 DE MAYO", "pre": 1910087489.39, "eje": 632010643.24, "fac": 706390410.75, "rf": 134602829.51, "ant": 817905939.0, "tr": 952508768.51}, {"c": "CRE01372024", "d": "ATLANTICO", "m": "BARANOA", "p": "SBN VILLA SOL", "pre": 444327614.43, "eje": 159830358.16, "fac": null, "rf": null, "ant": null, "tr": null}, {"c": "CRE01332024", "d": "MAGDALENA", "m": "CIENAGA", "p": "LA CONCEPCION", "pre": 1377665240.62, "eje": 391530752.56, "fac": 418259167.26, "rf": 0, "ant": 484288436.0, "tr": 484288436.0}, {"c": "CRE01422024", "d": "MAGDALENA", "m": "CIENAGA", "p": "DIVINO NIÑO", "pre": 875404285.52, "eje": 313890987.73, "fac": 410936461.04, "rf": 59847250.71, "ant": 475809718.0, "tr": 535656968.71}, {"c": "CRE01422024", "d": "MAGDALENA", "m": "CIENAGA", "p": "GIRASOLES", "pre": 494261406.8, "eje": 153694934.11, "fac": null, "rf": null, "ant": null, "tr": null}, {"c": "CRE01442024", "d": "MAGDALENA", "m": "CIENAGA", "p": "5 DE FEBRERO", "pre": 280216158.35, "eje": 85907249.66, "fac": 268551569.39, "rf": 102975809.56, "ant": 466420450.0, "tr": 569396259.56}, {"c": "CRE01442024", "d": "MAGDALENA", "m": "CIENAGA", "p": "LA FLORESTA", "pre": 196450926.28, "eje": 73363098.23, "fac": null, "rf": null, "ant": null, "tr": null}, {"c": "CRE01442024", "d": "MAGDALENA", "m": "CIENAGA", "p": "SAN JUAN", "pre": 865970664.56, "eje": 230483647.91, "fac": null, "rf": null, "ant": null, "tr": null}, {"c": "CRE01262024", "d": "ATLANTICO", "m": "LURUACO", "p": "FEDERICO CERVANTES EL CARMEN", "pre": 498607740.9, "eje": 185048288.29, "fac": 224395006.46, "rf": 27385638.77, "ant": 173213030.0, "tr": 200598668.77}, {"c": "CRE01232024", "d": "LA GUAJIRA", "m": "MAICAO", "p": "SANTA ISABEL", "pre": 2034930076.37, "eje": 712683999.62, "fac": 407022419.1, "rf": 172269532.41, "ant": 706916666.0, "tr": 879186198.4}, {"c": "CRE01282024", "d": "LA GUAJIRA", "m": "MAICAO", "p": "LOS LAURELES", "pre": 315058434.94, "eje": 123421276.41, "fac": 94526123.89, "rf": 40476619.11, "ant": 109448668.0, "tr": 149925287.11}, {"c": "CRE01402024", "d": "LA GUAJIRA", "m": "MAICAO", "p": "LA MOSCA", "pre": 680783109.43, "eje": 221322230.08, "fac": 330113111.13, "rf": 0, "ant": 573340558.0, "tr": 573340558.0}, {"c": "CRE01402024", "d": "LA GUAJIRA", "m": "MAICAO", "p": "PASTRANA", "pre": 633479248.19, "eje": 205419238.79, "fac": null, "rf": null, "ant": null, "tr": null}, {"c": "CRE01402024", "d": "LA GUAJIRA", "m": "MAICAO", "p": "RINCON GUAPO", "pre": 336157089.39, "eje": 107192867.17, "fac": null, "rf": null, "ant": null, "tr": null}, {"c": "CRE01352024", "d": "ATLANTICO", "m": "MALAMBO", "p": "SUBNORMAL CARACOLI", "pre": 1134910496.29, "eje": 436138178.75, "fac": 340504452.59, "rf": 61813968.0, "ant": 394258828.0, "tr": 456072796.0}, {"c": "CRE01292024", "d": "ATLANTICO", "m": "POLONUEVO", "p": "06 DE NOVIEMBRE", "pre": 417998133.23, "eje": 142318381.53, "fac": 125410738.52, "rf": 26315360.38, "ant": 145208941.0, "tr": 171524301.38}, {"c": "CRE01242024", "d": "ATLANTICO", "m": "PUERTO COLOMBIA", "p": "COLINAS DEL SOL", "pre": 1009310039.27, "eje": 376137036.69, "fac": 454230142.83, "rf": 77218809.83, "ant": 350625359.0, "tr": 427844168.83}, {"c": "CRE01342024", "d": "ATLANTICO", "m": "PUERTO COLOMBIA", "p": "SOLIMAR", "pre": 1411583214.06, "eje": 505693024.24, "fac": 423512842.7, "rf": 180790162.09, "ant": 490371493.0, "tr": 671161655.09}, {"c": "CRE01382024", "d": "LA GUAJIRA", "m": "RIOHACHA", "p": "NUEVO HORIZONTE", "pre": 146527812.8, "eje": 48806873.13, "fac": 158200170.48, "rf": 43615623.3, "ant": 274762107.0, "tr": 318377730.3}, {"c": "CRE01382024", "d": "LA GUAJIRA", "m": "RIOHACHA", "p": "VILLA JARDIN", "pre": 644402035.91, "eje": 239122934.47, "fac": null, "rf": null, "ant": null, "tr": null}, {"c": "CRE01272024", "d": "ATLANTICO", "m": "SABANALARGA", "p": "NOGALES", "pre": 245885224.0, "eje": 83645780.98, "fac": 484001841.6, "rf": 75334452.83, "ant": 373606468.0, "tr": 448940920.83}, {"c": "CRE01272024", "d": "ATLANTICO", "m": "SABANALARGA", "p": "VEINTE DE ENERO", "pre": 829570799.55, "eje": 300823962.06, "fac": null, "rf": null, "ant": null, "tr": null}, {"c": "CRE01392024", "d": "ATLANTICO", "m": "SABANALARGA", "p": "REY JOSE", "pre": 251189880.61, "eje": 94740210.63, "fac": 329836297.06, "rf": 66708157.8, "ant": 381906524.0, "tr": 448614681.8}, {"c": "CRE01392024", "d": "ATLANTICO", "m": "SABANALARGA", "p": "VILLA CAROLINA", "pre": 848160730.92, "eje": 327223518.93, "fac": null, "rf": null, "ant": null, "tr": 0}, {"c": "CRE01412024", "d": "ATLANTICO", "m": "SABANALARGA", "p": "CASCAJAL", "pre": 735432237.51, "eje": 286065825.59, "fac": 483213442.03, "rf": 68172292.01, "ant": 372997893.0, "tr": 441170185.01}, {"c": "CRE01412024", "d": "ATLANTICO", "m": "SABANALARGA", "p": "LAS AMERICAS", "pre": 338279500.78, "eje": 135465987.37, "fac": null, "rf": null, "ant": null, "tr": null}, {"c": "CRE01432024", "d": "ATLANTICO", "m": "SABANALARGA", "p": "VILLA ASPROS", "pre": 344316969.2, "eje": 143243194.43, "fac": 154956723.51, "rf": 0, "ant": 119612838.0, "tr": 119612838.0}, {"c": "CRE01302024", "d": "MAGDALENA", "m": "SANTA MARTA", "p": "GAIRA SECTOR VISTA DEL MAR", "pre": 886181407.87, "eje": 299667159.1, "fac": 177249832.0, "rf": 58469477.18, "ant": 307847564.0, "tr": 366317041.18}, {"c": "CRE01252024", "d": "ATLANTICO", "m": "SITIONUEVO", "p": "SIMON BOLIVAR", "pre": 1100072400.37, "eje": 385762765.66, "fac": 495079386.81, "rf": 66202975.71, "ant": 382157349.0, "tr": 448360324.71}, {"c": "CRE01312024", "d": "ATLANTICO", "m": "SITIONUEVO", "p": "SAN JOSE", "pre": 838861766.37, "eje": 312636992.88, "fac": 251683015.79, "rf": 48935523.34, "ant": 291415427.0, "tr": 340350950.34}, {"c": "CRE01362024", "d": "ATLANTICO", "m": "SITIONUEVO", "p": "EL PROGRESO", "pre": 796780451.5, "eje": 278751824.98, "fac": 358586350.98, "rf": 51145315.3, "ant": 276796839.0, "tr": 327942154.3}];
var CONTRATOS_RAW = [{"c": "CRE01212024", "d": "MAGDALENA", "m": "CIENAGA", "rep": 1260209286.0, "antT": 441073250.1, "ap": 220906816.83, "ac": 220166433.27, "amo": 109625339.21, "amat": 134332140.79, "ataj": 243957480.0, "valCont": 977113285, "delta": 283096001}, {"c": "CRE01232024", "d": "LA GUAJIRA", "m": "MAICAO", "rep": 2019761904.0, "antT": 706916666.4, "ap": 354163704.43, "ac": 352752961.97, "amo": 175698660.78, "amat": 240843580.85, "ataj": 416542241.63, "valCont": 2740558538, "delta": -720796634}, {"c": "CRE01242024", "d": "ATLANTICO", "m": "PUERTO COLOMBIA", "rep": 1001786739.0, "antT": 350625358.65, "ap": 174054511.74, "ac": 176570846.91, "amo": 87145216.52, "amat": 75067081.91, "ataj": 162212298.43, "valCont": 1079454984, "delta": -77668245}, {"c": "CRE01252024", "d": "ATLANTICO", "m": "SITIONUEVO", "rep": 1091878141.0, "antT": 382157349.35, "ap": 191652893.83, "ac": 190504455.52, "amo": 94982248.52, "amat": 125829709.11, "ataj": 220811957.63, "valCont": 1154196783, "delta": -62318642}, {"c": "CRE01262024", "d": "ATLANTICO", "m": "LURUACO", "rep": 494894372.0, "antT": 173213030.2, "ap": 89336438.78, "ac": 83876591.42, "amo": 43050756.73, "amat": 57097323.96, "ataj": 100148080.7, "valCont": 530726966, "delta": -35832594}, {"c": "CRE01272024", "d": "ATLANTICO", "m": "SABANALARGA", "rep": 1067447051.0, "antT": 373606467.85, "ap": 193153605.81, "ac": 180452862.04, "amo": 92856993.17, "amat": 137367972.53, "ataj": 230224965.69, "valCont": 1149875384, "delta": -82428333}, {"c": "CRE01282024", "d": "LA GUAJIRA", "m": "MAICAO", "rep": 312710479.0, "antT": 109448667.65, "ap": 59076188.92, "ac": 50372478.73, "amo": 27202618.42, "amat": 36708973.72, "ataj": 63911592.14, "valCont": 816076295, "delta": -503365816}, {"c": "CRE01292024", "d": "ATLANTICO", "m": "POLONUEVO", "rep": 414882688.0, "antT": 145208940.8, "ap": 74193181.23, "ac": 71015759.57, "amo": 36090557.27, "amat": 51461425.21, "ataj": 87551982.48, "valCont": 417935996, "delta": -3053308}, {"c": "CRE01302024", "d": "MAGDALENA", "m": "SANTA MARTA", "rep": 879564469.0, "antT": 307847564.15, "ap": 157176138.69, "ac": 150671425.46, "amo": 76513127.1, "amat": 88219460.41, "ataj": 164732587.51, "valCont": 751792515, "delta": 127771954}, {"c": "CRE01312024", "d": "ATLANTICO", "m": "SITIONUEVO", "rep": 832615506.0, "antT": 291415427.1, "ap": 145861321.73, "ac": 145554105.37, "amo": 72429046.74, "amat": 93374753.74, "ataj": 165803800.48, "valCont": 905675305, "delta": -73059799}, {"c": "CRE01332024", "d": "MAGDALENA", "m": "CIENAGA", "rep": 1383681246.0, "antT": 484288436.1, "ap": 242311058.24, "ac": 241977377.86, "amo": 120366138.9, "amat": 119815650.33, "ataj": 240181789.22, "valCont": 1479526255, "delta": -95845009}, {"c": "CRE01342024", "d": "ATLANTICO", "m": "PUERTO COLOMBIA", "rep": 1401061409.0, "antT": 490371493.15, "ap": 245836424.14, "ac": 244535069.01, "amo": 121878035.6, "amat": 140886055.85, "ataj": 262764091.45, "valCont": 2416671856, "delta": -1015610447}, {"c": "CRE01352024", "d": "ATLANTICO", "m": "MALAMBO", "rep": 1126453795.0, "antT": 394258828.25, "ap": 201597971.33, "ac": 192660856.92, "amo": 97989977.35, "amat": 117042035.06, "ataj": 215032012.41, "valCont": 1157893060, "delta": -31439265}, {"c": "CRE01362024", "d": "ATLANTICO", "m": "SITIONUEVO", "rep": 790848112.0, "antT": 276796839.2, "ap": 138859803.04, "ac": 137937036.16, "amo": 68795709.97, "amat": 83688958.3, "ataj": 152484668.27, "valCont": 866705494, "delta": -75857382}, {"c": "CRE01372024", "d": "ATLANTICO", "m": "BARANOA", "rep": 2336874112.0, "antT": 817905939.2, "ap": 413452654.34, "ac": 404453284.86, "amo": 203284184.68, "amat": 221149970.5, "ataj": 424434155.18, "valCont": 2432935792, "delta": -96061680}, {"c": "CRE01382024", "d": "LA GUAJIRA", "m": "RIOHACHA", "rep": 785034590.0, "antT": 274762106.5, "ap": 142005571.45, "ac": 132756535.05, "amo": 68289992.92, "amat": 96576113.66, "ataj": 164866106.59, "valCont": 787894296, "delta": -2859706}, {"c": "CRE01392024", "d": "ATLANTICO", "m": "SABANALARGA", "rep": 1091161498.0, "antT": 381906524.3, "ap": 198957819.61, "ac": 182948704.69, "amo": 94919907.9, "amat": 136859430.88, "ataj": 231779338.77, "valCont": 1150847371, "delta": -59685873}, {"c": "CRE01402024", "d": "LA GUAJIRA", "m": "MAICAO", "rep": 1638115879.0, "antT": 573340557.65, "ap": 291664972.58, "ac": 281675585.07, "amo": 142499353.8, "amat": 163782297.3, "ataj": 306281651.1, "valCont": 1621360186, "delta": 16755693}, {"c": "CRE01412024", "d": "ATLANTICO", "m": "SABANALARGA", "rep": 1065708265.0, "antT": 372997892.75, "ap": 196773246.16, "ac": 176224646.59, "amo": 92705736.54, "amat": 145823853.29, "ataj": 238529589.83, "valCont": 1977176250, "delta": -911467985}, {"c": "CRE01422024", "d": "MAGDALENA", "m": "CIENAGA", "rep": 1359456337.0, "antT": 475809717.95, "ap": 239907623.34, "ac": 235902094.61, "amo": 118258819.19, "amat": 164244827.47, "ataj": 282503646.66, "valCont": 1064770026, "delta": 294686311}, {"c": "CRE01432024", "d": "ATLANTICO", "m": "SABANALARGA", "rep": 341750967.0, "antT": 119612838.45, "ap": 66246113.69, "ac": 53366724.76, "amo": 29728844.33, "amat": 49472825.41, "ataj": 79201669.74, "valCont": 1313001661, "delta": -971250694}, {"c": "CRE01442024", "d": "MAGDALENA", "m": "CIENAGA", "rep": 1332629857.0, "antT": 466420449.95, "ap": 235821327.5, "ac": 230599122.45, "amo": 115925189.37, "amat": 155976362.84, "ataj": 271901552.2, "valCont": 1296926752, "delta": 35703105}];
var PROVEEDORES_RAW=[{"nom": "CAMEL", "mat": "POSTES CONCRETO", "presup": 1993388987.9, "final": 1812105820.6, "pag": 1812105820.6, "pct": 100.0}, {"nom": "HA", "mat": "HERRAJES", "presup": 4837505215.04, "final": 4837505215.04, "pag": 1621676694.19, "pct": 33.52}, {"nom": "INTERELECTRICAS", "mat": "PROTECCIONES", "presup": 225495770.76, "final": 225495770.76, "pag": 113086749.18, "pct": 50.15}, {"nom": "DESAAP", "mat": "POSTES FIBRA", "presup": 3213083678.54, "final": 3251804434.54, "pag": 1444449621.21, "pct": 44.42}, {"nom": "ESCAV INGENIERIA", "mat": "EXCAVACION", "presup": 136762000, "final": 136762000, "pag": 63127680, "pct": 46.16}];
var MO_RAW={"avanceObra": 0.35, "presup": 5247152286.98, "negoc": 5247152286.98, "ptoAvance": 1836503300.44, "gastoPagado": null, "items": [{"nom": "ADMINISTRACION", "presup": 1001143573, "negoc": 1001143573, "pto": 350400250.55, "gasto": null, "desv": 350400250.55}, {"nom": "ADM SOCIOS", "presup": 961141068.08, "negoc": 961141068.08, "pto": 336399373.83, "gasto": null, "desv": 336399373.83}, {"nom": "CTG (DA)", "presup": 2000000000, "negoc": 1000000000, "pto": 350000000, "gasto": 1000000000, "desv": -650000000}, {"nom": "CTG (VP)", "presup": 240000000, "negoc": 240000000, "pto": 84000000, "gasto": 80000000, "desv": 4000000}, {"nom": "CTG (DP)", "presup": 300000000, "negoc": 40000000, "pto": 14000000, "gasto": 40000000, "desv": -26000000}], "total": {"presup": 9449436928.06, "negoc": 8489436928.06, "pto": 2971302924.82, "gasto": 1120000000}};
var CAJA_RAW={"ingresos": 24028526702, "totalIngresos": 31176259750, "costos": 8804436928.06, "utilidad": 4684205232.12, "pctUtilidad": 19.49, "proveedores": 10539884541.83, "moTotal": 5247152286.98, "admin": 1001143573.0, "admSocios": 961141068.08, "saldoCaja": 655350029.76};
var ALL_DATA = PROJECTS_RAW.slice();
var CHARTS = {};

// ── GLOBAL FAC (Financiero) ───────────────────────────────
var FAC = {
  totalPresup:   24192535893.29,
  totalEje:       8471014872.07,
  totalFac:       7668063600.68,
  anticAmort:     3424601601.05,
  retegarantia:    761022578.01,
  retefuente:      152204515.60,
  reteIVA:          16813505.65,
  ICA:              60881806.24,
  netoRecibido:   1392034128.72,
  netoPendiente:  1860505465.41,
  anticipoTotal:  8409984345.00,
};
FAC.otrasRetencs = 221761994;
FAC.pendFacturar = FAC.totalEje - FAC.totalFac;
FAC.anticipoNoAmort = FAC.anticipoTotal - FAC.anticAmort;

// ── FORMATTERS ──────────────────────────────────────────
function fmtM(v){
  if(v==null||isNaN(v))return'-';
  var a=Math.abs(v);
  if(a>=1e9)return(v/1e9).toFixed(3)+' M';
  if(a>=1e6)return(v/1e6).toFixed(3)+' M';
  if(a>=1e3)return(v/1e3).toFixed(1)+' K';
  return Math.round(v).toLocaleString('es-CO');
}
function fmtPie(v){
  if(v==null||isNaN(v))return'-';
  var a=Math.abs(v);
  if(a>=1e9){
    // Miles de millones → 3 decimales (ej: 8.471 M, 3.424 M)
    return(v/1e9).toFixed(3)+' M';
  }
  if(a>=1e6){
    // Cientos de millones → sin decimales (ej: 761 M, 221 M, 802 M)
    return Math.round(v/1e6)+' M';
  }
  if(a>=1e3)return(v/1e3).toFixed(1)+' K';
  return Math.round(v).toLocaleString('es-CO');
}
function fmtF(v){
  if(v==null||isNaN(v))return'-';
  return Math.round(v).toLocaleString('es-CO');
}
function pct(a,b){return b&&b!==0?(a/b)*100:0;}
function semCol(p){return p>=38?'#1D9E75':p>=30?'#EF9F27':'#D85A30';}
function badge(d){
  var cl=d==='ATLANTICO'?'batl':d==='LA GUAJIRA'?'bgua':'bmag';
  return '<span class="badge '+cl+'">'+d.substring(0,3)+'</span>';
}
function chip(p){
  var cl=p>=38?'chi':p>=30?'chm':'chl';
  return '<span class="chip '+cl+'">'+p.toFixed(1)+'%</span>';
}
function semSt(r){
  if(r<80)return['Verde','sg'];
  if(r<=100)return['Amarillo','sy'];
  return['Rojo','sr'];
}
function mkChart(id,cfg){
  if(CHARTS[id]){CHARTS[id].destroy();delete CHARTS[id];}
  var ctx=document.getElementById(id);
  if(!ctx)return null;
  CHARTS[id]=new Chart(ctx,cfg);
  return CHARTS[id];
}
var gc='rgba(55,138,221,.1)',tc='#85C1E9',tf={size:9};
function xA(){return{ticks:{color:tc,font:tf},grid:{color:gc}};}
function yA(cb){return{ticks:{color:tc,font:tf,callback:cb||fmtM},grid:{color:gc}};}

// ── IMPORT ───────────────────────────────────────────────
function importExcel(evt){
  var file=evt.target.files[0]; if(!file)return;
  var st=document.getElementById('import-status');
  st.textContent='Cargando...';
  var reader=new FileReader();
  reader.onload=function(e){
    try{
      var wb=XLSX.read(e.target.result,{type:'array'});
      var ws=wb.Sheets[wb.SheetNames[0]];
      var rows=XLSX.utils.sheet_to_json(ws,{defval:null});
      if(!rows.length)throw new Error('Sin filas');
      function fk(row,keys){
        var rkeys=Object.keys(row);
        for(var i=0;i<keys.length;i++){
          var found=rkeys.find(function(rk){return rk.toLowerCase().indexOf(keys[i].toLowerCase())>=0;});
          if(found!==undefined)return row[found];
        }
        return null;
      }
      ALL_DATA=rows.map(function(r){
        var pre=+fk(r,['presupuesto replanteo','presupuesto'])||0;
        var eje=+fk(r,['valor ejecutado','ejecutado'])||0;
        return{
          c:String(fk(r,['contrato'])||''),
          d:String(fk(r,['departamento'])||'').toUpperCase().trim(),
          m:String(fk(r,['municipio'])||'').toUpperCase().trim(),
          p:String(fk(r,['proyecto'])||'').toUpperCase().trim(),
          pre:pre,eje:eje,pend:pre-eje,
          pct_proy:pre>0?pct(eje,pre):0,
          fac:fk(r,['valor facturado','facturado'])!=null?+fk(r,['valor facturado','facturado']):null,
          rf:fk(r,['valor recibidos','recibido'])!=null?+fk(r,['valor recibidos','recibido']):null,
          ant:fk(r,['valor anticipo recibido','anticipo recibido'])!=null?+fk(r,['valor anticipo recibido','anticipo recibido']):null,
          tr:fk(r,['valor total recibido','total recibido'])!=null?+fk(r,['valor total recibido','total recibido']):null,
          ap:null,ac:null,amo:null,amat:null,ataj:null,antT:null,rep:null
        };
      }).filter(function(r){return r.p;});
      st.textContent='Cargados '+ALL_DATA.length+' proyectos';
      resetAll();
    }catch(err){st.textContent='Error: '+err.message;}
  };
  reader.readAsArrayBuffer(file);
}

// ── FILTROS ──────────────────────────────────────────────
function populate(){
  var ids=['f0','f1','f2','f3'],keys=['d','m','c','p'];
  var saved=ids.map(function(id){return document.getElementById(id).value;});
  ids.forEach(function(id){var s=document.getElementById(id);while(s.options.length>1)s.remove(1);});
  var src=ALL_DATA;
  keys.forEach(function(k,i){
    var vals=[];
    var seen={};
    src.forEach(function(r){if(r[k]&&!seen[r[k]]){seen[r[k]]=1;vals.push(r[k]);}});
    vals.sort().forEach(function(v){document.getElementById(ids[i]).add(new Option(v,v));});
    if(saved[i])src=src.filter(function(r){return r[k]===saved[i];});
  });
  ids.forEach(function(id,i){if(saved[i])document.getElementById(id).value=saved[i];});
}
function applyFilters(){
  var v=['f0','f1','f2','f3'].map(function(id){return document.getElementById(id).value;});
  return ALL_DATA.filter(function(r){
    return(!v[0]||r.d===v[0])&&(!v[1]||r.m===v[1])&&(!v[2]||r.c===v[2])&&(!v[3]||r.p===v[3]);
  });
}
function cascade(){populate();render();}
function resetAll(){['f0','f1','f2','f3'].forEach(function(id){document.getElementById(id).value='';});populate();render();}

// ── RENDER ───────────────────────────────────────────────
function render(){
  var data=applyFilters();
  var active=['f0','f1','f2','f3'].map(function(id){return document.getElementById(id).value;}).filter(Boolean);
  document.getElementById('fstatus').textContent=data.length+' proyectos'+(active.length?' - '+active.join(' - '):'');
  renderKPIs(data);
  renderResumen(data);
  renderEjecucion(data);
  renderRecaudo(data);
  renderSemaforo(data);
  renderCompras(data);
  renderManoObra(data);
  renderProyectos(data);
  renderMunicipios(data);
}

// ── KPI STRIP ────────────────────────────────────────────
function renderKPIs(data){
  var pre=data.reduce(function(s,r){return s+r.pre;},0);
  var eje=data.reduce(function(s,r){return s+r.eje;},0);
  var fac=data.reduce(function(s,r){return s+(r.fac||0);},0);
  var tr=data.reduce(function(s,r){return s+(r.tr||0);},0);
  var pend=pre-eje,pe=pct(eje,pre);
  var kpis=[
    {cls:'k-b',lbl:'Presupuesto Total',val:fmtM(pre),sub:'100% del contrato',p:100},
    {cls:'k-g',lbl:'Valor Ejecutado',val:fmtM(eje),sub:pe.toFixed(1)+'% del presupuesto',p:pe},
    {cls:'k-a',lbl:'Total Facturado',val:fmtM(fac),sub:pct(fac,pre).toFixed(1)+'% del presupuesto',p:pct(fac,pre)},
    {cls:'k-p',lbl:'Total Recibido',val:fmtM(tr),sub:'Anticipo + rec. factura',p:pct(tr,pre)},
    {cls:'k-o',lbl:'Pendiente de lo Facturado',val:fmtM(FAC.netoPendiente),sub:'Por recibir sobre lo facturado',p:FAC.totalFac>0?Math.min(100,pct(FAC.netoPendiente,FAC.totalFac)):0},
    {cls:'k-p',lbl:'% Avance',val:'35%',sub:'Avance de obra a la fecha',p:35},
  ];
  document.getElementById('kpis-ejec-top').style.gridTemplateColumns='repeat(6,1fr)';
  document.getElementById('kpis-ejec-top').innerHTML=kpis.map(function(k){
    return '<div class="kpi '+k.cls+'"><div class="kpi-lbl">'+k.lbl+'</div><div class="kpi-val">'+k.val+'</div><div class="kpi-sub">'+k.sub+'</div><div class="kpi-bar" style="width:'+Math.min(100,k.p)+'%"></div></div>';
  }).join('');
}

// ── RESUMEN ──────────────────────────────────────────────
function renderResumen(data){
  var pre=data.reduce(function(s,r){return s+r.pre;},0);
  var eje=data.reduce(function(s,r){return s+r.eje;},0);
  var fac=data.reduce(function(s,r){return s+(r.fac||0);},0);
  var tr=data.reduce(function(s,r){return s+(r.tr||0);},0);
  var ant=data.reduce(function(s,r){return s+(r.ant||0);},0);
  var rf=data.reduce(function(s,r){return s+(r.rf||0);},0);
  var pend=pre-eje;

  // Total strip
  var strip=document.getElementById('total-strip');
  if(strip){
    strip.innerHTML=[
      {l:'Presupuesto Total',v:fmtF(pre),s:'100%'},
      {l:'Valor Ejecutado',v:fmtF(eje),s:pct(eje,pre).toFixed(2)+'% ejec.'},
      {l:'Pendiente x Ejecutar',v:fmtF(pend),s:pct(pend,pre).toFixed(2)+'% pend.'},
      {l:'Total Facturado',v:fmtF(fac),s:pct(fac,pre).toFixed(2)+'% del pres.'},
      {l:'Anticipo Recibido',v:fmtF(ant),s:pct(ant,pre).toFixed(2)+'% del pres.'},
      {l:'Recibido x Factura',v:fmtF(rf),s:pct(rf,fac||1).toFixed(2)+'% del fac.'},
      {l:'Total Recibido',v:fmtF(tr),s:pct(tr,pre).toFixed(2)+'% del pres.'},
    ].map(function(i){return '<div class="ts-item"><div class="ts-lbl">'+i.l+'</div><div class="ts-val">'+i.v+'</div><div class="ts-sub">'+i.s+'</div></div>';}).join('');
  }

  var deptsAll={};
  data.forEach(function(r){if(!deptsAll[r.d])deptsAll[r.d]={pre:0,eje:0,tr:0};deptsAll[r.d].pre+=r.pre;deptsAll[r.d].eje+=r.eje;deptsAll[r.d].tr+=r.tr||0;});
  document.getElementById('fin-cards').innerHTML='';
  // Fixed order: Atlantico, Magdalena, Guajira
  var FIXED_ORDER=['ATLANTICO','MAGDALENA','LA GUAJIRA'];
  var depts={};
  FIXED_ORDER.forEach(function(d){depts[d]=deptsAll[d]||{pre:0,eje:0,tr:0};});
  // Also add any department not in fixed list
  Object.keys(deptsAll).forEach(function(d){if(FIXED_ORDER.indexOf(d)<0)depts[d]=deptsAll[d];});
  var dKeys=FIXED_ORDER.filter(function(d){return deptsAll[d];});
  Object.keys(deptsAll).forEach(function(d){if(FIXED_ORDER.indexOf(d)<0)dKeys.push(d);});

  // Barras horizontales avance por departamento
  var deptColors=dKeys.map(function(d){var p=pct(depts[d].eje,depts[d].pre);return semCol(p);});
  mkChart('dept-prog-bar',{type:'bar',data:{
    labels:dKeys,
    datasets:[
      {label:'Ejecutado',data:dKeys.map(function(d){return depts[d].eje;}),backgroundColor:deptColors,borderRadius:4},
      {label:'Presupuesto',data:dKeys.map(function(d){return depts[d].pre;}),backgroundColor:'rgba(55,138,221,.12)',borderRadius:4}
    ]
  },options:{
    indexAxis:'y',responsive:true,maintainAspectRatio:false,
    plugins:{
      legend:{display:true,labels:{color:tc,font:tf}},
      datalabels:{display:false},
      tooltip:{callbacks:{label:function(ctx){
        var d=dKeys[ctx.dataIndex];
        var p=pct(depts[d].eje,depts[d].pre);
        if(ctx.datasetIndex===0)return[ctx.dataset.label+': '+fmtM(ctx.raw),'Avance: '+p.toFixed(2)+'%'];
        return ctx.dataset.label+': '+fmtM(ctx.raw);
      }}}
    },
    scales:{
      x:{ticks:{color:tc,font:tf,callback:fmtM},grid:{color:gc}},
      y:{ticks:{color:tc,font:{size:11},font:{weight:'600'}},grid:{display:false}}
    }
  }});

  // Control Costos por Dpto. Presupuesto vs Real
  var AVANCE_OBRA = 0.35;
  mkChart('bar-dept',{type:'bar',data:{labels:dKeys,datasets:[
    {label:'Ejecutado (Real)',data:dKeys.map(function(d){return depts[d].eje;}),backgroundColor:'#378ADD',borderRadius:3},
    {label:'Meta 35% Presupuesto',data:dKeys.map(function(d){return depts[d].pre*AVANCE_OBRA;}),backgroundColor:'rgba(29,158,117,.25)',borderRadius:3,borderColor:'rgba(29,158,117,.6)',borderWidth:1}
  ]},options:{
    plugins:{
      legend:{display:true,labels:{color:tc,font:tf}},
      datalabels:{display:false},
      tooltip:{callbacks:{label:function(ctx){
        var d=dKeys[ctx.dataIndex];
        if(ctx.datasetIndex===0){
          var meta=depts[d].pre*AVANCE_OBRA;
          var diff=depts[d].eje-meta;
          var sign=diff>=0?'+':'';
          return[ctx.dataset.label+': '+fmtM(ctx.raw),'vs meta: '+sign+fmtM(diff)+' ('+sign+pct(diff,meta).toFixed(1)+'%)'];
        }
        return ctx.dataset.label+': '+fmtM(ctx.raw);
      }}}
    },
    scales:{x:xA(),y:yA()}
  }});

  // Torta costos por departamento
  var pieColors=['#378ADD','#EF9F27','#1D9E75','#534AB7','#D85A30'];
  var totalEjeDpts=dKeys.reduce(function(s,d){return s+depts[d].eje;},0);
  mkChart('pie-costos-dpto',{type:'doughnut',data:{
    labels:dKeys,
    datasets:[{data:dKeys.map(function(d){return depts[d].eje;}),backgroundColor:pieColors,borderWidth:1,borderColor:'rgba(20,30,45,0.9)',hoverOffset:8}]
  },options:{
    responsive:true,maintainAspectRatio:false,
    plugins:{
      legend:{display:false},
      tooltip:{callbacks:{label:function(ctx){return ctx.label+': '+fmtM(ctx.raw)+' ('+pct(ctx.raw,totalEjeDpts).toFixed(1)+'%)';}}}
    },
    cutout:'55%'
  }});
  document.getElementById('pie-costos-dpto-leg').innerHTML=dKeys.map(function(d,i){
    return '<span class="litem" style="font-size:11px"><span class="lsq" style="background:'+pieColors[i]+';width:12px;height:12px;border-radius:3px"></span><strong style="color:#E2E8F0">'+d+'</strong> &nbsp;<span style="color:#85C1E9">'+fmtM(depts[d].eje)+'</span> <span style="color:'+pieColors[i]+';font-weight:700">('+pct(depts[d].eje,totalEjeDpts).toFixed(1)+'%)</span></span>';
  }).join('');
  mkChart('pie-rec',{type:'doughnut',data:{labels:['Anticipo Recibido','Recibido x Factura','Pendiente'],datasets:[{data:[ant,rf,Math.max(0,pre-tr)],backgroundColor:['#EF9F27','#1D9E75','rgba(55,138,221,.2)'],borderWidth:0}]},options:{plugins:{legend:{display:false},tooltip:{callbacks:{label:function(ctx){return ctx.label+': '+fmtF(ctx.raw);}}}},cutout:'60%'}});
  document.getElementById('pie-rec-leg').innerHTML=[['Anticipo','#EF9F27'],['Rec. Factura','#1D9E75'],['Pendiente','rgba(55,138,221,.4)']].map(function(a){return '<span class="litem"><span class="lsq" style="background:'+a[1]+'"></span>'+a[0]+'</span>';}).join('');
  document.getElementById('kpi-stats').innerHTML=[
    ['Proyectos filtrados',String(data.length),''],
    ['% ejec. ponderado',pct(eje,pre).toFixed(2)+'%',''],
    ['Pendiente ejecutar',fmtF(pend),'neg'],
    ['Brecha ejec.-facturado',fmtF(eje-fac),eje>fac?'neg':'pos'],
    ['Anticipo / Presupuesto',pct(ant,pre).toFixed(2)+'%',''],
    ['Recibido / Ejecutado',pct(tr,eje).toFixed(2)+'%',''],
    ['Deuda de recaudo',fmtF(fac-rf),'neg'],
  ].map(function(a){return '<div class="stat-row"><span class="stat-lbl">'+a[0]+'</span><span class="stat-val '+a[2]+'">'+a[1]+'</span></div>';}).join('');


  // ── KPI AVANCE FINANCIERO ─────────────────────────────────
  // (FAC is now defined globally above)
  var pctEjecFin = pct(FAC.totalEje, FAC.totalPresup);

  // KPI cards — 4 tarjetas (sin Presupuesto Total ni Neto Recibido)
  var finKpiData = [
    {cls:'kpc kcg', lbl:'% Ejecutado', val:pctEjecFin.toFixed(1)+'%', sub:fmtM(FAC.totalEje)+' ejecutado', p:pctEjecFin},
    {cls:'kpc kcy', lbl:'Total Facturado', val:fmtM(FAC.totalFac), sub:pct(FAC.totalFac,FAC.totalEje).toFixed(1)+'% del ejecutado', p:pct(FAC.totalFac,FAC.totalEje)},
    {cls:'kpc kcp', lbl:'Anticipo Recibido', val:fmtM(FAC.anticipoTotal), sub:'Amortizado: '+fmtM(FAC.anticAmort), p:pct(FAC.anticAmort,FAC.anticipoTotal)},
    {cls:'kpc kco', lbl:'Pendiente por Recibir', val:fmtM(FAC.netoPendiente), sub:'Neto pendiente de cobro', p:pct(FAC.netoPendiente,FAC.totalFac)},
  ];
  document.getElementById('fin-kpi-strip').innerHTML = finKpiData.map(function(k){
    return '<div class="'+k.cls+'"><div class="kpc-title">'+k.lbl+'</div><div class="kpc-val" style="font-size:16px">'+k.val+'</div><div class="kpc-sub">'+k.sub+'</div><div class="kpc-bar"><div class="kpc-fill" style="width:'+Math.min(100,k.p)+'%"></div></div></div>';
  }).join('');

  // TORTA 1: EJECUCION — 100% = Total Ejecutado
  // Segmentos: Anticipo amortizado | Retegarantia | Otras retenciones | Ingreso recibido | Pendiente por recibir | Pendiente por facturar
  mkChart('pie-ejec',{
    type:'doughnut',
    data:{
      labels:[
        'Anticipo amortizado',
        'Retegarantia',
        'Otras retenciones',
        'Ingreso por factura recibido',
        'Pendiente por ingresar (neto)',
        'Pendiente por facturar'
      ],
      datasets:[{
        data:[
          FAC.anticAmort,
          FAC.retegarantia,
          FAC.otrasRetencs,
          FAC.netoRecibido,
          FAC.netoPendiente,
          FAC.pendFacturar
        ],
        backgroundColor:['#EF9F27','#D85A30','#F0997B','#1D9E75','rgba(29,158,117,.35)','rgba(55,138,221,.25)'],
        borderWidth:1, borderColor:'rgba(20,30,45,0.9)', hoverOffset:8
      }]
    },
    options:{
      responsive:true, maintainAspectRatio:false,
      plugins:{
        legend:{display:false},
        tooltip:{callbacks:{label:function(ctx){
          return ctx.label+': '+fmtM(ctx.raw)+' ('+pct(ctx.raw,FAC.totalEje).toFixed(1)+'%)';
        }}},
        datalabels:{
          display:true,
          color:'#fff',font:{weight:'bold',size:9},
          formatter:function(v,ctx){
            var total=ctx.chart.data.datasets[0].data.reduce(function(a,b){return a+b;},0);
            var p=pct(v,total);
            if(p<5)return'';
            return fmtPie(v);
          },
          textAlign:'center'
        }
      },
      cutout:'55%',
      centerText: fmtPie(FAC.totalEje)
    }
  });
  document.getElementById('pie-ejec-leg').innerHTML=[
    ['Anticipo amortizado','#EF9F27'],
    ['Retegarantia','#D85A30'],
    ['Otras retenciones','#F0997B'],
    ['Ingreso recibido','#1D9E75'],
    ['Pend. por ingresar','rgba(29,158,117,.6)'],
    ['Pend. por facturar','rgba(55,138,221,.5)']
  ].map(function(a){
    return '<span class="litem" style="font-size:9px"><span class="lsq" style="background:'+a[1]+';width:8px;height:8px"></span>'+a[0]+'</span>';
  }).join('');

  // TORTA 2: RECAUDO — segmentos sobre lo facturado + anticipo
  // Segmentos: Anticipo ya amortizado | Anticipo disponible (no amortizado) | Recibido por factura | Pendiente por recibir
  mkChart('pie-recaudo',{
    type:'doughnut',
    data:{
      labels:[
        'Anticipo amortizado en facturas',
        'Anticipo',
        'Ingreso por factura real',
        'Pendiente por recibir real'
      ],
      datasets:[{
        data:[
          FAC.anticAmort,
          FAC.anticipoTotal,
          FAC.netoRecibido,
          FAC.netoPendiente
        ],
        backgroundColor:['#EF9F27','rgba(239,159,39,.35)','#1D9E75','rgba(216,90,48,.55)'],
        borderWidth:1, borderColor:'rgba(20,30,45,0.9)', hoverOffset:8
      }]
    },
    options:{
      responsive:true, maintainAspectRatio:false,
      plugins:{
        legend:{display:false},
        tooltip:{callbacks:{label:function(ctx){
          var base = FAC.anticipoTotal + FAC.netoRecibido + FAC.netoPendiente;
          return ctx.label+': '+fmtM(ctx.raw)+' ('+pct(ctx.raw,base).toFixed(1)+'%)';
        }}},
        datalabels:{
          display:true,
          color:'#fff',font:{weight:'bold',size:9},
          formatter:function(v,ctx){
            var total=ctx.chart.data.datasets[0].data.reduce(function(a,b){return a+b;},0);
            var p=pct(v,total);
            if(p<5)return'';
            return fmtPie(v);
          },
          textAlign:'center'
        }
      },
      cutout:'55%',
      centerText: fmtPie(FAC.anticipoTotal + FAC.netoRecibido)
    }
  });
  document.getElementById('pie-recaudo-leg').innerHTML=[
    ['Anticipo amortizado','#EF9F27'],
    ['Anticipo','rgba(239,159,39,.6)'],
    ['Recibido por factura','#1D9E75'],
    ['Pendiente por recibir','rgba(216,90,48,.75)']
  ].map(function(a){
    return '<span class="litem" style="font-size:9px"><span class="lsq" style="background:'+a[1]+';width:8px;height:8px"></span>'+a[0]+'</span>';
  }).join('');

  // ── KPI COMPRAS en Resumen ────────────────────────────────
  var totPresupP=PROVEEDORES_RAW.reduce(function(s,r){return s+r.presup;},0);
  var totPagP=PROVEEDORES_RAW.reduce(function(s,r){return s+(r.pag||0);},0);
  var totPendP=totPresupP-totPagP;
  var pctPagP=pct(totPagP,totPresupP);
  var variP=totPagP-totPresupP;
  function semChip(pv,hi,med){
    if(pv>=hi)return'<span class="chip chi">Verde '+pv.toFixed(1)+'%</span>';
    if(pv>=med)return'<span class="chip chm">Amarillo '+pv.toFixed(1)+'%</span>';
    return'<span class="chip chl">Bajo '+pv.toFixed(1)+'%</span>';
  }
  var compKpiData=[
    {cls:'k-b',lbl:'Presupuesto Inicial',val:fmtM(totPresupP),sub:'Total inicial proveedores',p:100},
    {cls:'k-p',lbl:'Presupuesto Actual',val:fmtM(PROVEEDORES_RAW.reduce(function(s,r){return s+(r.final||0);},0)),sub:'Presupuesto negociado final',p:pct(PROVEEDORES_RAW.reduce(function(s,r){return s+(r.final||0);},0),totPresupP)},
    {cls:'k-g',lbl:'Total Pagado',val:fmtM(totPagP),sub:pctPagP.toFixed(1)+'% del presupuesto',p:pctPagP},
    {cls:'k-a',lbl:'% Pagado / Presupuesto',val:pctPagP.toFixed(1)+'%',sub:'Avance de compras global',p:Math.min(100,pctPagP)},
    {cls:variP<0?'k-g':'k-o',lbl:'Variacion',val:fmtM(Math.abs(variP)),sub:variP<0?'Pagado menor al presup.':'Pagado supera presupuesto',p:Math.min(100,Math.abs(pct(variP,totPresupP)))},
  ];
  document.getElementById('res-comp-kpis').innerHTML=compKpiData.map(function(k){
    return '<div class="kpi '+k.cls+'"><div class="kpi-lbl">'+k.lbl+'</div><div class="kpi-val" style="font-size:14px">'+k.val+'</div><div class="kpi-sub">'+k.sub+'</div><div class="kpi-bar" style="width:'+Math.min(100,k.p)+'%"></div></div>';
  }).join('');
  mkChart('res-comp-bar',{type:'bar',data:{
    labels:PROVEEDORES_RAW.map(function(r){return r.nom;}),
    datasets:[
      {label:'Presup. Inicial',data:PROVEEDORES_RAW.map(function(r){return r.presup;}),backgroundColor:'rgba(55,138,221,.35)',borderRadius:3},
      {label:'Presup. Actual',data:PROVEEDORES_RAW.map(function(r){return r.final||0;}),backgroundColor:'rgba(83,74,183,.55)',borderRadius:3},
      {label:'% Avance en Pago',data:PROVEEDORES_RAW.map(function(r){return r.pct||0;}),backgroundColor:PROVEEDORES_RAW.map(function(r){var pv=r.pct||0;return pv>=75?'#1D9E75':pv>=40?'#EF9F27':'#D85A30';}),borderRadius:3,yAxisID:'y2'},
    ]},
    options:{responsive:true,maintainAspectRatio:false,
    plugins:{legend:{display:true,labels:{color:tc,font:tf}},datalabels:{display:false},tooltip:{callbacks:{label:function(ctx){
      if(ctx.datasetIndex===2)return ctx.dataset.label+': '+ctx.raw.toFixed(1)+'%';
      return ctx.dataset.label+': '+fmtM(ctx.raw);
    }}}}
    ,scales:{
      x:{ticks:{color:tc,font:tf},grid:{display:false}},
      y:{ticks:{color:tc,font:tf,callback:fmtM},grid:{color:gc}},
      y2:{position:'right',ticks:{color:'#EF9F27',font:tf,callback:function(v){return v+'%';}},grid:{display:false},min:0,max:120}
    }}});
  // ── KPI MANO DE OBRA en Resumen ──────────────────────────
  var mo=MO_RAW;
  var totGasto=mo.items.reduce(function(s,r){return s+(r.gasto||0);},0);
  var avancePct=mo.avanceObra*100;
  var pctGastoVsPto=pct(totGasto,mo.ptoAvance);
  var pctGastoVsPresup=pct(totGasto,mo.presup);
  var desviTotal=totGasto-mo.ptoAvance;
  var moKpiData=[
    {cls:'k-b',lbl:'Presupuesto Total MO',val:fmtM(mo.presup),sub:'Costo laboral proyectado 100% avance',p:100},
    {cls:'k-p',lbl:'Pto para avance 35%',val:fmtM(mo.ptoAvance),sub:pct(mo.ptoAvance,mo.presup).toFixed(1)+'% del presup. total',p:pct(mo.ptoAvance,mo.presup)},
    {cls:totGasto>0?'k-g':'k-a',lbl:'Gasto actual MO',val:totGasto>0?fmtM(totGasto):'Sin registro',sub:totGasto>0?(pctGastoVsPresup.toFixed(1)+'% del presup. total'):'Pagos no registrados en MO directa',p:Math.min(100,pctGastoVsPresup)},
    {cls:desviTotal>0?'k-o':'k-g',lbl:'Desviacion vs Pto avance',val:fmtM(Math.abs(desviTotal)),sub:desviTotal>0?'⚠ Gasto supera pto del avance':desviTotal<0?'✓ Por debajo del pto':'En linea con avance',p:Math.min(100,Math.abs(pctGastoVsPto))},
  ];
  document.getElementById('res-mo-kpis').innerHTML=moKpiData.map(function(k){
    return '<div class="kpi '+k.cls+'"><div class="kpi-lbl">'+k.lbl+'</div><div class="kpi-val" style="font-size:14px">'+k.val+'</div><div class="kpi-sub">'+k.sub+'</div><div class="kpi-bar" style="width:'+Math.min(100,k.p)+'%"></div></div>';
  }).join('');
  // Collapse CTG items into a single Contingencia Total
  var ctgItems=mo.items.filter(function(r){return r.nom&&r.nom.indexOf('CTG')>=0;});
  var nonCtgItems=mo.items.filter(function(r){return !r.nom||r.nom.indexOf('CTG')<0;});
  var ctgTot={nom:'CONTINGENCIA TOTAL',presup:0,negoc:0,pto:0,gasto:0,desv:0};
  ctgItems.forEach(function(r){ctgTot.presup+=(r.presup||0);ctgTot.negoc+=(r.negoc||0);ctgTot.pto+=(r.pto||0);ctgTot.gasto+=(r.gasto||0);ctgTot.desv+=(r.desv||0);});

  // Helper to make a 3-bar chart for a single concept
  function mkMoConceptChart(canvasId, item) {
    var avancePctBar = item.pto && item.presup ? pct(item.pto, item.presup) : 0;
    mkChart(canvasId,{type:'bar',data:{
      labels:['Presup. Inicial MO','Presup. Actual MO','% Avance'],
      datasets:[{
        data:[item.presup||0, item.negoc||0, avancePctBar],
        backgroundColor:['rgba(55,138,221,.35)','rgba(83,74,183,.55)',(item.gasto&&item.gasto>item.pto)?'#D85A30':'#1D9E75'],
        borderRadius:4
      }]
    },options:{responsive:true,maintainAspectRatio:false,
      plugins:{legend:{display:false},tooltip:{callbacks:{label:function(ctx){
        if(ctx.dataIndex===2)return '% Avance: '+ctx.raw.toFixed(1)+'%';
        return ctx.dataset.label+': '+fmtM(ctx.raw);
      }}},datalabels:{display:true,color:'#fff',font:{weight:'bold',size:9},formatter:function(v,ctx){
        if(ctx.dataIndex===2)return v.toFixed(1)+'%';
        return fmtM(v);
      },anchor:'center',align:'center'}},
      scales:{x:{ticks:{color:tc,font:tf},grid:{display:false}},y:{ticks:{color:tc,font:tf,callback:fmtM},grid:{color:gc}}}
    }});
  }

  // Mano de Obra chart (using mo.presup and mo.negoc as the MO totals)
  var moDirecto={nom:'MANO DE OBRA',presup:mo.presup,negoc:mo.negoc,pto:mo.ptoAvance,gasto:totGasto};
  mkMoConceptChart('res-mo-bar', moDirecto);

  // Administracion
  var admItem=mo.items.find(function(r){return r.nom==='ADMINISTRACION';})||{presup:0,negoc:0,pto:0,gasto:0};
  mkMoConceptChart('res-adm-bar', admItem);

  // Administracion Socios
  var admSItem=mo.items.find(function(r){return r.nom==='ADM SOCIOS';})||{presup:0,negoc:0,pto:0,gasto:0};
  mkMoConceptChart('res-adms-bar', admSItem);

  // Contingencia Total
  mkMoConceptChart('res-ctg-bar', ctgTot);
}

// ── EJECUCION ────────────────────────────────────────────
function renderEjecucion(data){
  var wrap=document.getElementById('execbar-wrap');
  wrap.style.height=Math.max(220,data.length*22)+'px';
  mkChart('exec-bar',{type:'bar',data:{labels:data.map(function(r){return r.p.substring(0,24);}),datasets:[{label:'Ejecutado',data:data.map(function(r){return r.eje;}),backgroundColor:'#378ADD'},{label:'Pendiente',data:data.map(function(r){return Math.max(0,r.pre-r.eje);}),backgroundColor:'rgba(55,138,221,.15)'}]},options:{indexAxis:'y',responsive:true,maintainAspectRatio:false,scales:{x:{ticks:{color:tc,font:tf,callback:fmtM},grid:{color:gc},stacked:true},y:{ticks:{color:tc,font:{size:8}},grid:{display:false},stacked:true}},plugins:{legend:{display:false},tooltip:{callbacks:{label:function(ctx){return ctx.dataset.label+': '+fmtF(ctx.raw);}}}}}});
  mkChart('pct-bar',{type:'bar',data:{labels:data.map(function(r){return r.p.substring(0,22);}),datasets:[{label:'%',data:data.map(function(r){return pct(r.eje,r.pre);}),backgroundColor:data.map(function(r){return semCol(pct(r.eje,r.pre));})}]},options:{indexAxis:'y',responsive:true,maintainAspectRatio:false,scales:{x:{max:50,ticks:{color:tc,font:tf,callback:function(v){return v+'%';}},grid:{color:gc}},y:{ticks:{color:tc,font:{size:7}},grid:{display:false}}},plugins:{legend:{display:false},tooltip:{callbacks:{label:function(ctx){return ctx.raw.toFixed(2)+'%';}}}}}});
  var te=data.reduce(function(s,r){return s+r.eje;},0),tp=data.reduce(function(s,r){return s+r.pre;},0);
  mkChart('exec-donut',{type:'doughnut',data:{labels:['Ejecutado','Ingreso pendiente'],datasets:[{data:[te,Math.max(0,tp-te)],backgroundColor:['#1D9E75','rgba(55,138,221,.15)'],borderWidth:0}]},options:{plugins:{legend:{display:false},tooltip:{callbacks:{label:function(ctx){return ctx.label+': '+fmtF(ctx.raw)+' ('+pct(ctx.raw,tp).toFixed(2)+'%)';}}}},cutout:'65%',datalabels:{color:'#fff',font:{weight:'bold',size:9},formatter:function(v,ctx){var total=tp;var p=pct(v,total);if(p<5)return'';return fmtPie(v);},textAlign:'center'}}});
  document.getElementById('donut-leg').innerHTML=[['Ejecutado ('+pct(te,tp).toFixed(2)+'%)','#1D9E75'],['Ingreso pendiente ('+pct(tp-te,tp).toFixed(2)+'%)','rgba(55,138,221,.4)']].map(function(a){return '<span class="litem"><span class="lsq" style="background:'+a[1]+'"></span>'+a[0]+'</span>';}).join('');
  var el=document.getElementById('ejec-totals');
  if(el){el.innerHTML=[['Total Presupuesto',fmtM(tp),''],['Total Ejecutado',fmtM(te),'pos'],['Ingreso Pendiente',fmtM(tp-te),'neg']].map(function(a){return '<div class="stat-row"><span class="stat-lbl">'+a[0]+'</span><span class="stat-val '+a[2]+'">'+a[1]+'</span></div>';}).join('');}
}

// ── RECAUDO ──────────────────────────────────────────────
function renderRecaudo(data){
  var cont={};
  data.forEach(function(r){
    if(r.fac==null)return;
    if(!cont[r.c])cont[r.c]={fac:0,rf:0,ant:0,tr:0};
    cont[r.c].fac+=r.fac;
    cont[r.c].rf+=r.rf||0;
    cont[r.c].ant+=r.ant||0;
    cont[r.c].tr+=r.tr||0;
  });
  var cl=Object.keys(cont);
  mkChart('rec-bar',{type:'bar',data:{labels:cl.map(function(c){return c.replace('CRE0','');}),datasets:[{label:'Facturado',data:cl.map(function(c){return cont[c].fac;}),backgroundColor:'#378ADD'},{label:'Rec. Factura',data:cl.map(function(c){return cont[c].rf;}),backgroundColor:'#1D9E75'},{label:'Anticipo',data:cl.map(function(c){return cont[c].ant;}),backgroundColor:'#EF9F27'}]},options:{plugins:{legend:{display:true,labels:{color:tc,font:tf}}},scales:{x:xA(),y:yA()}}});
  var dFac=data.filter(function(r){return r.fac!=null;});
  mkChart('brecha-bar',{type:'bar',data:{labels:dFac.map(function(r){return r.p.substring(0,20);}),datasets:[{label:'Brecha Ejec.-Fac.',data:dFac.map(function(r){return (r.eje||0)-(r.fac||0);}),backgroundColor:dFac.map(function(r){return (r.eje||0)>(r.fac||0)?'#D85A30':'#1D9E75';})}]},options:{indexAxis:'y',responsive:true,maintainAspectRatio:false,scales:{x:{ticks:{color:tc,font:tf,callback:fmtM},grid:{color:gc}},y:{ticks:{color:tc,font:{size:8}},grid:{display:false}}},plugins:{legend:{display:false},tooltip:{callbacks:{label:function(ctx){return fmtF(ctx.raw);}}}}}});
  var totFac=0,totRF=0,totAnt=0,totTR=0;
  document.getElementById('rec-tbody').innerHTML=cl.map(function(c){
    var v=cont[c];totFac+=v.fac;totRF+=v.rf;totAnt+=v.ant;totTR+=v.tr;
    return '<tr><td style="font-size:10px">'+c+'</td><td class="r">'+fmtF(v.fac)+'</td><td class="r">'+fmtF(v.rf)+'</td><td class="r">'+fmtF(v.ant)+'</td><td class="r">'+fmtF(v.tr)+'</td></tr>';
  }).join('');
  document.getElementById('rec-tfoot').innerHTML='<td>TOTAL</td><td class="r">'+fmtF(totFac)+'</td><td class="r">'+fmtF(totRF)+'</td><td class="r">'+fmtF(totAnt)+'</td><td class="r">'+fmtF(totTR)+'</td>';
}

// ── SEMAFORO ─────────────────────────────────────────────
function renderSemaforo(data){
  var rows=data.map(function(r){
    var tr=r.tr||0,eje=r.eje||0;
    var ratio=tr>0?pct(eje,tr):eje>0?999:0;
    var st=semSt(ratio);
    return{p:r.p,d:r.d,c:r.c,pre:r.pre,eje:eje,tr:tr,ratio:ratio,diff:tr-eje,lbl:st[0],dot:st[1],pctEje:pct(eje,r.pre)};
  }).sort(function(a,b){return b.ratio-a.ratio;});
  var verde=rows.filter(function(r){return r.ratio<80;}).length;
  var amar=rows.filter(function(r){return r.ratio>=80&&r.ratio<=100;}).length;
  var rojo=rows.filter(function(r){return r.ratio>100;}).length;
  mkChart('sem-donut',{type:'doughnut',data:{labels:['Verde ('+verde+')','Amarillo ('+amar+')','Rojo ('+rojo+')'],datasets:[{data:[verde,amar,rojo],backgroundColor:['#1D9E75','#EF9F27','#D85A30'],borderWidth:0}]},options:{plugins:{legend:{display:false}},cutout:'55%'}});
  document.getElementById('sem-donut-leg').innerHTML=[['Verde','#1D9E75'],['Amarillo','#EF9F27'],['Rojo','#D85A30']].map(function(a){return '<span class="litem"><span class="lsq" style="background:'+a[1]+'"></span>'+a[0]+'</span>';}).join('');
  var hasRec=rows.filter(function(r){return r.tr>0;}).slice(0,16);
  mkChart('sem-bar',{type:'bar',data:{labels:hasRec.map(function(r){return r.p.substring(0,16);}),datasets:[{label:'Total a Recibir',data:hasRec.map(function(r){return r.tr;}),backgroundColor:'rgba(55,138,221,.25)'},{label:'Ya Ejecutado',data:hasRec.map(function(r){return r.eje;}),backgroundColor:hasRec.map(function(r){return r.eje>r.tr?'#D85A30':r.tr>0&&r.eje/r.tr>0.8?'#EF9F27':'#1D9E75';})}]},options:{plugins:{legend:{display:true,labels:{color:tc,font:tf}},tooltip:{callbacks:{label:function(ctx){return ctx.dataset.label+': '+fmtF(ctx.raw);}}}},scales:{x:xA(),y:yA()}}});
  var totTR=rows.reduce(function(s,r){return s+(r.tr||0);},0);
  var totE=rows.reduce(function(s,r){return s+r.eje;},0);
  document.getElementById('sem-tbody').innerHTML=rows.map(function(r){
    var col=r.ratio<80?'#1D9E75':r.ratio<=100?'#EF9F27':'#D85A30';
    var bg=r.dot==='sg'?'#1D9E75':r.dot==='sy'?'#EF9F27':'#D85A30';
    return '<tr><td><span style="display:inline-block;width:12px;height:12px;border-radius:50%;background:'+bg+';vertical-align:middle;margin-right:4px;box-shadow:0 0 4px '+bg+'"></span>'+r.lbl+'</td>'
      +'<td style="max-width:170px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;font-size:11px">'+r.p+'</td>'
      +'<td>'+badge(r.d)+'</td>'
      +'<td style="font-size:10px">'+r.c+'</td>'
      +'<td class="r">'+(r.tr?fmtF(r.tr):'-')+'</td>'
      +'<td class="r">'+fmtF(r.eje)+'</td>'
      +'<td class="r '+(r.diff>=0?'pos':'neg')+'">'+(r.tr?fmtF(r.diff):'-')+'</td>'
      +'<td class="r" style="color:'+col+';font-weight:700">'+(r.tr?r.ratio.toFixed(2)+'%':'N/A')+'</td>'
      +'<td class="r">'+chip(r.pctEje)+'</td></tr>';
  }).join('');
  document.getElementById('sem-tfoot').innerHTML='<td colspan="4">TOTAL ('+rows.length+' proyectos)</td>'
    +'<td class="r">'+fmtF(totTR)+'</td>'
    +'<td class="r">'+fmtF(totE)+'</td>'
    +'<td class="r '+(totTR>=totE?'pos':'neg')+'">'+fmtF(totTR-totE)+'</td>'
    +'<td class="r">'+pct(totE,totTR).toFixed(2)+'%</td><td></td>';
}

// ── COMPRAS ──────────────────────────────────────────────
function renderCompras(data){
  var sel={};data.forEach(function(r){sel[r.c]=1;});
  var cRows=CONTRATOS_RAW.filter(function(r){return sel[r.c]&&r.antT>0;});
  var totPresupP=PROVEEDORES_RAW.reduce(function(s,r){return s+r.presup;},0);
  var totPagP=PROVEEDORES_RAW.reduce(function(s,r){return s+(r.pag||0);},0);
  var tAnt=cRows.reduce(function(s,r){return s+r.antT;},0);
  var tProv=cRows.reduce(function(s,r){return s+r.ap;},0);
  var tCont=cRows.reduce(function(s,r){return s+r.ac;},0);
  var pprov=pct(tProv,tAnt),pcont=pct(tCont,tAnt),vari=tProv-tCont;
  var pendAnt=Math.max(0,tAnt-tProv-tCont);
  document.getElementById('compras-kpi-grid').innerHTML=[
    {cls:'kcb',t:'Anticipo Total Proyectado',v:fmtF(tAnt),s:cRows.length+' contratos',p:100},
    {cls:'kcg',t:'Pagado a Proveedores',v:fmtF(tProv),s:pprov.toFixed(2)+'% del anticipo total',p:pprov},
    {cls:'kcp',t:'Pagado a Contratistas',v:fmtF(tCont),s:pcont.toFixed(2)+'% del anticipo total',p:pcont},
    {cls:'kcy',t:'% Compras / Anticipo',v:pprov.toFixed(2)+'%',s:'Participacion proveedores',p:pprov},
    {cls:'kco',t:'Variacion Prov. - Cont.',v:fmtF(Math.abs(vari)),s:vari>=0?'Proveedor > Contratista':'Contratista > Proveedor',p:Math.min(100,Math.abs(pct(vari,tAnt)))},
    {cls:'kcb',t:'Pendiente de Compra',v:fmtF(Math.max(0,totPresupP-totPagP)),s:pct(Math.max(0,totPresupP-totPagP),totPresupP).toFixed(2)+'% sin comprar',p:pct(Math.max(0,totPresupP-totPagP),totPresupP)},
  ].map(function(k){return '<div class="kpc '+k.cls+'"><div class="kpc-title">'+k.t+'</div><div class="kpc-val">'+k.v+'</div><div class="kpc-sub">'+k.s+'</div><div class="kpc-bar"><div class="kpc-fill" style="width:'+Math.min(100,k.p)+'%"></div></div></div>';}).join('');
  var top=cRows.slice().sort(function(a,b){return b.antT-a.antT;});
  mkChart('compras-bar',{type:'bar',data:{labels:top.map(function(r){return r.c.replace('CRE0','');}),datasets:[{label:'A Proveedor',data:top.map(function(r){return r.ap;}),backgroundColor:'#1D9E75'},{label:'A Contratista',data:top.map(function(r){return r.ac;}),backgroundColor:'#534AB7'},{label:'Anticipo Total',data:top.map(function(r){return r.antT;}),backgroundColor:'rgba(55,138,221,.15)'}]},options:{plugins:{legend:{display:true,labels:{color:tc,font:tf}},tooltip:{callbacks:{label:function(ctx){return ctx.dataset.label+': '+fmtF(ctx.raw);}}}},scales:{x:xA(),y:yA()}}});
  mkChart('compras-donut',{type:'doughnut',data:{labels:['A Proveedor','A Contratista'],datasets:[{data:[tProv,tCont],backgroundColor:['#1D9E75','#534AB7'],borderWidth:0}]},options:{plugins:{legend:{display:false},datalabels:{display:false},tooltip:{callbacks:{label:function(ctx){return ctx.label+': '+fmtM(ctx.raw)+' ('+pct(ctx.raw,tAnt).toFixed(1)+'%)';}}}},cutout:'60%'}});
  document.getElementById('compras-donut-leg').innerHTML=[['A Proveedor ('+pprov.toFixed(2)+'%)','#1D9E75'],['A Contratista ('+pcont.toFixed(2)+'%)','#534AB7']].map(function(a){return '<span class="litem"><span class="lsq" style="background:'+a[1]+'"></span>'+a[0]+'</span>';}).join('');
  mkChart('compras-pct-bar',{type:'bar',data:{labels:cRows.map(function(r){return r.c.replace('CRE0','');}),datasets:[{label:'% A Proveedor',data:cRows.map(function(r){return pct(r.ap,r.antT);}),backgroundColor:cRows.map(function(r){var p=pct(r.ap,r.antT);return p>=55?'#1D9E75':p>=45?'#EF9F27':'#D85A30';})}]},options:{plugins:{legend:{display:false},tooltip:{callbacks:{label:function(ctx){return ctx.raw.toFixed(2)+'%';}}}},scales:{x:xA(),y:{ticks:{color:tc,font:tf,callback:function(v){return v.toFixed(0)+'%';}},grid:{color:gc}}}}});
  document.getElementById('compras-tbody').innerHTML=cRows.map(function(r){
    var pp=pct(r.ap,r.antT),pc=pct(r.ac,r.antT),va=r.ap-r.ac;
    return '<tr><td style="font-size:10px">'+r.c+'</td><td class="r">'+fmtF(r.antT)+'</td><td class="r">'+fmtF(r.ap)+'</td><td class="r" style="color:'+(pp>=50?'#5FD4A8':'#FAC775')+'">'+pp.toFixed(2)+'%</td><td class="r">'+fmtF(r.ac)+'</td><td class="r">'+pc.toFixed(2)+'%</td><td class="r '+(va>=0?'pos':'neg')+'">'+fmtF(va)+'</td></tr>';
  }).join('');
  document.getElementById('compras-tfoot').innerHTML='<td>TOTAL</td><td class="r">'+fmtF(tAnt)+'</td><td class="r">'+fmtF(tProv)+'</td><td class="r">'+pprov.toFixed(2)+'%</td><td class="r">'+fmtF(tCont)+'</td><td class="r">'+pcont.toFixed(2)+'%</td><td class="r '+(vari>=0?'pos':'neg')+'">'+fmtF(vari)+'</td>';
}

// ── MANO DE OBRA ─────────────────────────────────────────
function buildEjeByC(data){
  var m={};
  data.forEach(function(r){if(!m[r.c])m[r.c]={eje:0,pre:0};m[r.c].eje+=r.eje||0;m[r.c].pre+=r.pre||0;});
  return m;
}
var MU_MAP={'212':'CIENAGA','232':'MAICAO','242':'P.COLOMBIA','252':'SITIONUEVO','262':'LURUACO','272':'SABANALARGA','282':'MAICAO','292':'POLONUEVO','302':'STA.MARTA','312':'SITIONUEVO','332':'CIENAGA','342':'P.COLOMBIA','352':'MALAMBO','362':'SITIONUEVO','372':'BARANOA','382':'RIOHACHA','392':'SABANALARGA','402':'MAICAO','412':'SABANALARGA','422':'CIENAGA','432':'SABANALARGA','442':'CIENAGA'};

function renderManoObra(data){
  var sel={};data.forEach(function(r){sel[r.c]=1;});
  var eByC=buildEjeByC(data);
  var cRows=CONTRATOS_RAW.filter(function(r){return sel[r.c]&&r.rep>0;});
  var tMO=cRows.reduce(function(s,r){return s+r.amo;},0);
  var tMat=cRows.reduce(function(s,r){return s+r.amat;},0);
  var tAdj=cRows.reduce(function(s,r){return s+r.ataj;},0);
  var tRep=cRows.reduce(function(s,r){return s+r.rep;},0);
  var tEje=cRows.reduce(function(s,r){return s+(eByC[r.c]?eByC[r.c].eje:0);},0);
  var pMO=pct(tMO,tEje),pAvg=pct(tEje,tRep),pAdj=pct(tAdj,tRep);
  document.getElementById('mo-kpi-grid').innerHTML=[
    {cls:'kcp',t:'Ajuste MO Presupuestado',v:fmtF(tMO),s:pMO.toFixed(2)+'% del ejecutado total',p:Math.min(100,pMO)},
    {cls:'kcy',t:'Ajuste Materiales',v:fmtF(tMat),s:pct(tMat,tAdj).toFixed(2)+'% del ajuste total',p:pct(tMat,tAdj)},
    {cls:'kcb',t:'Total Ajuste MO + Materiales',v:fmtF(tAdj),s:pAdj.toFixed(2)+'% del replanteo',p:Math.min(100,pAdj)},
    {cls:'kcg',t:'Valor Ejecutado Total',v:fmtF(tEje),s:pAvg.toFixed(2)+'% del presupuesto replanteo',p:Math.min(100,pAvg)},
    {cls:'kco',t:'% MO / Ejecutado',v:pMO.toFixed(2)+'%',s:'Costo laboral sobre avance real',p:Math.min(100,pMO)},
    {cls:'kcb',t:'Ingreso Pendiente',v:fmtF(Math.max(0,tRep-tEje)),s:pct(tRep-tEje,tRep).toFixed(2)+'% del replanteo',p:Math.min(100,pct(tRep-tEje,tRep))},
  ].map(function(k){return '<div class="kpc '+k.cls+'"><div class="kpc-title">'+k.t+'</div><div class="kpc-val">'+k.v+'</div><div class="kpc-sub">'+k.s+'</div><div class="kpc-bar"><div class="kpc-fill" style="width:'+Math.min(100,k.p)+'%"></div></div></div>';}).join('');
  var top=cRows.slice().sort(function(a,b){return b.rep-a.rep;});
  mkChart('mo-bar',{type:'bar',data:{labels:top.map(function(r){return r.c.replace('CRE0','');}),datasets:[{label:'Presup. Replanteo',data:top.map(function(r){return r.rep;}),backgroundColor:'rgba(55,138,221,.2)'},{label:'Ajuste MO',data:top.map(function(r){return r.amo;}),backgroundColor:'#534AB7'},{label:'Ejecutado',data:top.map(function(r){return eByC[r.c]?eByC[r.c].eje:0;}),backgroundColor:'#1D9E75'}]},options:{plugins:{legend:{display:true,labels:{color:tc,font:tf}},tooltip:{callbacks:{label:function(ctx){return ctx.dataset.label+': '+fmtF(ctx.raw);}}}},scales:{x:xA(),y:yA()}}});
  var pArr=cRows.map(function(r){var e=eByC[r.c]?eByC[r.c].eje:0;return{c:r.c.replace('CRE0',''),v:e?pct(r.amo,e):0,av:r.rep?pct(e,r.rep):0};});
  mkChart('mo-pct-bar',{type:'bar',data:{labels:pArr.map(function(r){return r.c;}),datasets:[{label:'% MO/Ejecutado',data:pArr.map(function(r){return r.v;}),backgroundColor:pArr.map(function(r){return r.v>35?'#D85A30':r.v>25?'#EF9F27':'#1D9E75';})}]},options:{plugins:{legend:{display:false},tooltip:{callbacks:{label:function(ctx){return ctx.raw.toFixed(2)+'%';}}}},scales:{x:xA(),y:{ticks:{color:tc,font:tf,callback:function(v){return v.toFixed(0)+'%';}},grid:{color:gc}}}}});
  mkChart('mo-donut',{type:'doughnut',data:{labels:['Ajuste MO','Ajuste Materiales'],datasets:[{data:[tMO,tMat],backgroundColor:['#534AB7','#EF9F27'],borderWidth:0}]},options:{plugins:{legend:{display:false},tooltip:{callbacks:{label:function(ctx){return ctx.label+': '+fmtF(ctx.raw)+' ('+pct(ctx.raw,tAdj).toFixed(2)+'%)';}}}},cutout:'60%'}});
  document.getElementById('mo-donut-leg').innerHTML=[['Ajuste MO ('+pct(tMO,tAdj).toFixed(2)+'%)','#534AB7'],['Ajuste Materiales ('+pct(tMat,tAdj).toFixed(2)+'%)','#EF9F27']].map(function(a){return '<span class="litem"><span class="lsq" style="background:'+a[1]+'"></span>'+a[0]+'</span>';}).join('');
  mkChart('mo-scatter',{type:'scatter',data:{datasets:[{label:'Contratos',data:pArr.filter(function(r){return r.av>0;}).map(function(r){return{x:r.av,y:r.v,c:r.c};}),backgroundColor:'rgba(83,74,183,.7)',pointRadius:6,pointHoverRadius:8}]},options:{plugins:{legend:{display:false},tooltip:{callbacks:{label:function(ctx){return ctx.raw.c+' | Avance: '+ctx.raw.x.toFixed(2)+'% | MO: '+ctx.raw.y.toFixed(2)+'%';}}}},scales:{x:{title:{display:true,text:'% Avance de Obra',color:tc,font:tf},ticks:{color:tc,font:tf,callback:function(v){return v.toFixed(0)+'%';}},grid:{color:gc}},y:{title:{display:true,text:'% MO / Ejecutado',color:tc,font:tf},ticks:{color:tc,font:tf,callback:function(v){return v.toFixed(0)+'%';}},grid:{color:gc}}}}});
  document.getElementById('mo-tbody').innerHTML=cRows.map(function(r){
    var e=eByC[r.c]?eByC[r.c].eje:0;
    var pM=e?pct(r.amo,e):0,pA=r.rep?pct(e,r.rep):0;
    var key=r.c.replace('CRE0','').substring(0,3);
    var mu=MU_MAP[key]||'';
    var cM=pM>35?'#F0997B':pM>25?'#EF9F27':'#5FD4A8';
    return '<tr><td style="font-size:10px">'+r.c+'</td><td style="font-size:10px">'+mu+'</td>'
      +'<td class="r">'+fmtF(r.rep)+'</td>'
      +'<td class="r" style="color:#9D97E8">'+fmtF(r.amo)+'</td>'
      +'<td class="r" style="color:#EF9F27">'+fmtF(r.amat)+'</td>'
      +'<td class="r">'+fmtF(r.ataj)+'</td>'
      +'<td class="r">'+fmtF(e)+'</td>'
      +'<td class="r" style="color:'+cM+';font-weight:700">'+pM.toFixed(2)+'%</td>'
      +'<td class="r" style="color:'+semCol(pA)+';font-weight:700">'+pA.toFixed(2)+'%</td>'
      +'<td>'+chip(pA)+'</td></tr>';
  }).join('');
  document.getElementById('mo-tfoot').innerHTML='<td>TOTAL</td><td></td>'
    +'<td class="r">'+fmtF(tRep)+'</td>'
    +'<td class="r">'+fmtF(tMO)+'</td>'
    +'<td class="r">'+fmtF(tMat)+'</td>'
    +'<td class="r">'+fmtF(tAdj)+'</td>'
    +'<td class="r">'+fmtF(tEje)+'</td>'
    +'<td class="r">'+pMO.toFixed(2)+'%</td>'
    +'<td class="r">'+pAvg.toFixed(2)+'%</td><td></td>';
}

// ── PROYECTOS ────────────────────────────────────────────
function renderProyectos(data){
  document.getElementById('tbl-count').textContent=data.length+' proyectos';
  var tp=0,te=0,tpend=0,tf=0,ta=0,tr=0;
  document.getElementById('full-tbody').innerHTML=data.map(function(r){
    var p=pct(r.eje,r.pre);
    tp+=r.pre;te+=r.eje;tpend+=r.pend;tf+=r.fac||0;ta+=r.ant||0;tr+=r.tr||0;
    return '<tr><td style="max-width:170px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap;font-size:11px">'+r.p+'</td>'
      +'<td>'+badge(r.d)+'</td>'
      +'<td style="font-size:10px">'+r.m+'</td>'
      +'<td style="font-size:9px">'+r.c+'</td>'
      +'<td class="r">'+fmtF(r.pre)+'</td>'
      +'<td class="r">'+fmtF(r.eje)+'</td>'
      +'<td class="r">'+fmtM(r.pend)+'</td>'
      +'<td class="r">'+chip(p)+'</td>'
      +'<td class="r">'+(r.fac!=null?fmtF(r.fac):'-')+'</td>'
      +'<td class="r">'+(r.ant!=null?fmtF(r.ant):'-')+'</td>'
      +'<td class="r">'+(r.tr!=null?fmtF(r.tr):'-')+'</td>'
      +'<td>'+chip(p)+'</td></tr>';
  }).join('');
  document.getElementById('full-tfoot').innerHTML='<td colspan="4">TOTAL ('+data.length+' proyectos)</td>'
    +'<td class="r">'+fmtF(tp)+'</td>'
    +'<td class="r">'+fmtF(te)+'</td>'
    +'<td class="r">'+fmtF(tpend)+'</td>'
    +'<td class="r">'+pct(te,tp).toFixed(2)+'%</td>'
    +'<td class="r">'+fmtF(tf)+'</td>'
    +'<td class="r">'+fmtF(ta)+'</td>'
    +'<td class="r">'+fmtF(tr)+'</td><td></td>';
}

// ── MUNICIPIOS ────────────────────────────────────────────
function renderMunicipios(data){
  var munis={};
  data.forEach(function(r){if(!munis[r.m])munis[r.m]={d:r.d,pre:0,eje:0,tr:0,n:0};munis[r.m].pre+=r.pre;munis[r.m].eje+=r.eje;munis[r.m].tr+=r.tr||0;munis[r.m].n++;});
  var ml=Object.keys(munis).sort(function(a,b){return munis[b].pre-munis[a].pre;});
  var wrap=document.getElementById('muni-bar-wrap');
  wrap.style.height=Math.max(220,ml.length*26)+'px';
  mkChart('muni-bar',{type:'bar',data:{labels:ml,datasets:[{label:'Ejecutado',data:ml.map(function(m){return munis[m].eje;}),backgroundColor:'#378ADD'},{label:'Presupuesto',data:ml.map(function(m){return munis[m].pre;}),backgroundColor:'rgba(55,138,221,.15)'}]},options:{indexAxis:'y',responsive:true,maintainAspectRatio:false,scales:{x:{ticks:{color:tc,font:tf,callback:fmtM},grid:{color:gc}},y:{ticks:{color:tc,font:{size:9}},grid:{display:false}}},plugins:{legend:{display:true,labels:{color:tc,font:tf}},tooltip:{callbacks:{label:function(ctx){return ctx.dataset.label+': '+fmtF(ctx.raw);}}}}}});
  var totPre=0,totEje=0;
  document.getElementById('muni-tbody').innerHTML=ml.map(function(m){
    var v=munis[m],p=pct(v.eje,v.pre);
    totPre+=v.pre;totEje+=v.eje;
    return '<tr><td style="font-weight:600">'+m+'</td><td>'+badge(v.d)+'</td><td class="r">'+fmtF(v.pre)+'</td><td class="r">'+fmtF(v.eje)+'</td><td class="r">'+chip(p)+'</td><td style="text-align:center;font-weight:700">'+v.n+'</td></tr>';
  }).join('');
  document.getElementById('muni-tfoot').innerHTML='<td>TOTAL</td><td></td><td class="r">'+fmtF(totPre)+'</td><td class="r">'+fmtF(totEje)+'</td><td class="r">'+pct(totEje,totPre).toFixed(2)+'%</td><td style="text-align:center">'+data.length+'</td>';
  mkChart('muni-rec',{type:'bar',data:{labels:ml,datasets:[{label:'Total Recibido',data:ml.map(function(m){return munis[m].tr;}),backgroundColor:'#1D9E75'}]},options:{plugins:{legend:{display:false},tooltip:{callbacks:{label:function(ctx){return fmtF(ctx.raw);}}}},scales:{x:xA(),y:yA()}}});
}

// ── TABS ──────────────────────────────────────────────────
function showTab(i){
  document.querySelectorAll('.tab').forEach(function(t,j){t.classList.toggle('active',i===j);});
  document.querySelectorAll('.view').forEach(function(v,j){v.classList.toggle('active',i===j);});
}

window.addEventListener('DOMContentLoaded',function(){populate();render();});
</script>

<div style="margin-top:18px;padding:10px 16px;border-top:1px solid rgba(55,138,221,.15);display:flex;justify-content:flex-end">
  <span style="font-size:10px;color:rgba(133,193,233,.4);font-style:italic;letter-spacing:.06em">Created by: Carlos A. Torres</span>
</div>

</div>
</body>
</html>
