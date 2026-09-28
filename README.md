<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Sistem Lelang Online Transparan & Monitoring</title>

    <style>
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            min-height: 100vh;
            background: radial-gradient(ellipse at top left, rgba(43, 112, 220, 0.16), transparent 42%),
                        linear-gradient(135deg, #f3f7ff 0%, #eef3f9 55%, #f8fafc 100%);
            padding: 36px 20px;
            color: #17243a;
        }

        .container {
            max-width: 960px;
            margin: 0 auto;
        }

        .card {
            background: white;
            padding: 28px;
            border-radius: 16px;
            margin-bottom: 20px;
            box-shadow: 0 16px 45px rgba(31, 54, 91, 0.10);
            border: 1px solid rgba(220, 229, 241, 0.8);
        }

        #authSection {
            max-width: 760px;
            margin: 4vh auto 0;
            padding: 0;
            overflow: hidden;
        }

        .home-hero {
            position: relative;
            overflow: hidden;
            padding: 38px 38px 32px;
            color: white;
            background: linear-gradient(125deg, #123b78, #1769c2 62%, #35a5c9);
        }

        .home-hero::after {
            content: "";
            position: absolute;
            width: 230px;
            height: 230px;
            right: -65px;
            top: -95px;
            border: 1px solid rgba(255,255,255,0.22);
            border-radius: 50%;
            box-shadow: 0 0 0 28px rgba(255,255,255,0.06), 0 0 0 58px rgba(255,255,255,0.04);
        }

        .hero-eyebrow {
            display: inline-block;
            margin-bottom: 14px;
            padding: 6px 11px;
            border: 1px solid rgba(255,255,255,0.35);
            border-radius: 30px;
            background: rgba(255,255,255,0.12);
            font-size: 0.78rem;
            font-weight: 700;
            letter-spacing: 0.08em;
            text-transform: uppercase;
        }

        .home-hero h1 {
            max-width: 530px;
            margin-bottom: 12px;
            font-size: clamp(1.8rem, 5vw, 2.55rem);
            line-height: 1.15;
        }

        .home-hero p {
            max-width: 540px;
            color: rgba(255,255,255,0.86);
            line-height: 1.65;
        }

        .hero-highlights {
            display: flex;
            flex-wrap: wrap;
            gap: 10px;
            margin-top: 22px;
        }

        .hero-highlights span {
            padding: 8px 11px;
            border-radius: 7px;
            background: rgba(255,255,255,0.13);
            font-size: 0.85rem;
        }

        .auth-content {
            padding: 28px 38px 30px;
        }

        .auth-content h2 {
            margin-bottom: 6px;
        }

        .auth-subtitle {
            margin-bottom: 16px;
            color: #6b778c;
            font-size: 0.92rem;
            line-height: 1.5;
        }

        h2, h3, h4 {
            margin-bottom: 15px;
            color: #1a1a1a;
        }

        label {
            font-size: 0.9em;
            font-weight: bold;
            color: #555;
            display: block;
            margin-top: 10px;
        }

        input,
        textarea,
        button {
            width: 100%;
            padding: 12px;
            margin: 6px 0 12px 0;
            border: 1px solid #ccc;
            border-radius: 6px;
            font-size: 14px;
        }

        textarea {
            min-height: 110px;
            resize: vertical;
            border-color: #d8e0eb;
            background: #fbfcfe;
            transition: border-color 0.2s, box-shadow 0.2s;
        }

        textarea:focus {
            outline: none;
            border-color: #3984e6;
            box-shadow: 0 0 0 3px rgba(13, 110, 253, 0.12);
            background: white;
        }

        button {
            background-color: #0d6efd;
            color: white;
            border: none;
            cursor: pointer;
            font-weight: bold;
            transition: 0.2s;
        }

        button:hover {
            background-color: #0b5ed7;
            transform: translateY(-1px);
        }

        input {
            border-color: #d8e0eb;
            background: #fbfcfe;
            transition: border-color 0.2s, box-shadow 0.2s;
        }

        input:focus {
            outline: none;
            border-color: #3984e6;
            box-shadow: 0 0 0 3px rgba(13, 110, 253, 0.12);
            background: white;
        }

        .btn-danger {
            background-color: #dc3545;
        }

        .btn-danger:hover {
            background-color: #bb2d3b;
        }

        .btn-success {
            background-color: #198754;
        }

        .btn-success:hover {
            background-color: #157347;
        }

        .btn-secondary {
            background-color: #6c757d;
        }

        .btn-warning {
            background-color: #ffc107;
            color: #212529;
        }

        .hidden {
            display: none !important;
        }

        /* TAB MENU & AUTH TABS */
        .admin-tabs, .auth-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }

        .admin-tabs button, .auth-tabs button {
            margin: 0;
            background-color: #e9ecef;
            color: #333;
        }

        .admin-tabs button.active, .auth-tabs button.active {
            background-color: #0d6efd;
            color: white;
            box-shadow: 0 4px 10px rgba(13, 110, 253, 0.18);
        }

        .auth-tabs button {
            padding: 11px 14px;
            border-radius: 8px;
        }

        /* FOTO */
        .main-image {
            width: 100%;
            height: 320px;
            object-fit: cover;
            border-radius: 8px;
            border: 1px solid #e0e0e0;
            margin-bottom: 10px;
        }

        .gallery-thumbs {
            display: flex;
            gap: 10px;
            overflow-x: auto;
            padding-bottom: 8px;
            margin-bottom: 15px;
        }

        .thumb-img {
            width: 80px;
            height: 80px;
            object-fit: cover;
            border-radius: 6px;
            cursor: pointer;
            border: 2px solid transparent;
            opacity: 0.7;
            transition: 0.2s;
            flex-shrink: 0;
        }

        .thumb-img.active,
        .thumb-img:hover {
            opacity: 1;
            border-color: #0d6efd;
        }

        /* TIMER */
        .timer-box {
            padding: 12px;
            border-radius: 6px;
            text-align: center;
            font-weight: bold;
            margin-bottom: 15px;
            font-size: 1.1em;
        }

        .status-running {
            background: #fff3cd;
            color: #856404;
            border: 1px solid #ffeeba;
        }

        .status-ended {
            background: #f8d7da;
            color: #842029;
            border: 1px solid #f5c2c7;
            font-size: 1.3em;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .status-waiting {
            background: #e2e3e5;
            color: #41464b;
            border: 1px solid #d3d6d8;
        }

        .winner-box {
            background: #d1e7dd;
            color: #0f5132;
            padding: 15px;
            border-radius: 6px;
            text-align: center;
            font-weight: bold;
            margin-bottom: 15px;
            border: 1px solid #badbcc;
            font-size: 1.1em;
        }

        .price {
            font-size: 1.4em;
            color: #198754;
            font-weight: bold;
        }

        .badge {
            display: inline-block;
            padding: 4px 8px;
            background: #e9ecef;
            border-radius: 4px;
            font-size: 0.8em;
            color: #495057;
        }

        /* BID */
        .bid-history {
            margin-top: 20px;
            border-top: 2px solid #f0f0f0;
            padding-top: 15px;
        }

        .bid-list {
            list-style: none;
            max-height: 250px;
            overflow-y: auto;
        }

        .bid-item {
            padding: 12px;
            border-bottom: 1px solid #eee;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .bid-item:first-child {
            background-color: #e8f5e9;
            font-weight: bold;
            border-radius: 6px;
        }

        .bid-time {
            font-size: 0.8em;
            color: #6c757d;
        }

        /* DASHBOARD PEMBELI */
        #userSection {
            padding: 0;
            overflow: hidden;
            border: 0;
        }

        .user-topbar {
            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: 16px;
            padding: 20px 30px;
            background: #fff;
            border-bottom: 1px solid #e8edf5;
        }

        .brand-lockup {
            display: flex;
            align-items: center;
            gap: 12px;
            color: #17345f;
            font-weight: 800;
            letter-spacing: -0.02em;
        }

        .brand-mark {
            display: grid;
            place-items: center;
            width: 40px;
            height: 40px;
            border-radius: 12px;
            color: white;
            background: linear-gradient(135deg, #1769c2, #35a5c9);
            box-shadow: 0 7px 16px rgba(23, 105, 194, 0.24);
        }

        .user-topbar .btn-danger {
            width: auto;
            margin: 0;
            padding: 9px 16px;
            border-radius: 8px;
        }

        .user-dashboard-content {
            padding: 28px 30px 32px;
            background: #f7f9fc;
        }

        .dashboard-hero {
            position: relative;
            overflow: hidden;
            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: 20px;
            padding: 30px;
            border-radius: 16px;
            color: white;
            background: linear-gradient(115deg, #123b78, #1769c2 65%, #35a5c9);
            box-shadow: 0 12px 28px rgba(23, 79, 145, 0.18);
        }

        .dashboard-hero::after {
            content: "";
            position: absolute;
            width: 220px;
            height: 220px;
            top: -110px;
            right: 8%;
            border: 1px solid rgba(255,255,255,0.2);
            border-radius: 50%;
            box-shadow: 0 0 0 28px rgba(255,255,255,0.05), 0 0 0 58px rgba(255,255,255,0.04);
            pointer-events: none;
        }

        .dashboard-hero-copy {
            position: relative;
            z-index: 1;
        }

        .dashboard-kicker {
            display: block;
            margin-bottom: 9px;
            color: #b9e8ff;
            font-size: 0.78rem;
            font-weight: 800;
            letter-spacing: 0.12em;
            text-transform: uppercase;
        }

        .dashboard-hero h1 {
            margin-bottom: 8px;
            color: white;
            font-size: clamp(1.55rem, 4vw, 2.15rem);
            line-height: 1.2;
        }

        .dashboard-hero p {
            max-width: 520px;
            color: rgba(255,255,255,0.82);
            line-height: 1.6;
        }

        .hero-emblem {
            position: relative;
            z-index: 1;
            display: grid;
            place-items: center;
            flex: 0 0 82px;
            width: 82px;
            height: 82px;
            border: 1px solid rgba(255,255,255,0.35);
            border-radius: 24px;
            background: rgba(255,255,255,0.14);
            font-size: 2.5rem;
            transform: rotate(5deg);
        }

        .dashboard-stats {
            display: grid;
            grid-template-columns: repeat(4, minmax(0, 1fr));
            gap: 14px;
            margin: 18px 0 28px;
        }

        .dashboard-stat {
            display: flex;
            align-items: center;
            gap: 13px;
            width: 100%;
            min-height: 84px;
            margin: 0;
            padding: 16px;
            border: 1px solid #e7edf5;
            border-radius: 12px;
            background: white;
            color: inherit;
            text-align: left;
            box-shadow: 0 5px 16px rgba(31, 54, 91, 0.04);
            transition: border-color 0.2s, box-shadow 0.2s, transform 0.2s;
        }

        .dashboard-stat:hover,
        .dashboard-stat.active {
            border-color: #80b5ef;
            background: white;
            color: inherit;
            box-shadow: 0 8px 20px rgba(31, 83, 145, 0.12);
            transform: translateY(-2px);
        }

        .dashboard-stat:focus-visible {
            outline: 3px solid rgba(13, 110, 253, 0.3);
            outline-offset: 2px;
        }

        .stat-icon {
            display: grid;
            place-items: center;
            flex: 0 0 42px;
            width: 42px;
            height: 42px;
            border-radius: 12px;
            color: #1769c2;
            background: #eaf3ff;
            font-size: 1.2rem;
        }

        .dashboard-stat strong {
            display: block;
            color: #1b2d49;
            font-size: 1.25rem;
        }

        .dashboard-stat span:last-child {
            color: #758198;
            font-size: 0.82rem;
        }

        .catalog-heading {
            display: flex;
            justify-content: space-between;
            align-items: end;
            gap: 12px;
            margin-bottom: 14px;
        }

        .catalog-heading h2 {
            margin: 0 0 4px;
            color: #1b2d49;
            font-size: 1.35rem;
        }

        .catalog-heading p {
            color: #78849a;
            font-size: 0.9rem;
        }

        .catalog-label {
            padding: 7px 11px;
            border-radius: 30px;
            color: #1769c2;
            background: #eaf3ff;
            font-size: 0.78rem;
            font-weight: 700;
            white-space: nowrap;
        }

        /* DAFTAR LELANG */
        .auction-list {
            display: grid;
            gap: 15px;
        }

        #userAuctionList {
            grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
            align-items: stretch;
        }

        .auction-card {
            border: 1px solid #e5ebf3;
            border-radius: 13px;
            padding: 17px;
            background: #fff;
            box-shadow: 0 6px 18px rgba(31, 54, 91, 0.05);
            transition: transform 0.2s, box-shadow 0.2s, border-color 0.2s;
        }

        #userAuctionList .auction-card:hover {
            transform: translateY(-3px);
            border-color: #bfd7f5;
            box-shadow: 0 12px 25px rgba(31, 83, 145, 0.11);
        }

        #userAuctionList .auction-card-image {
            width: 130px;
            height: 105px;
            border-radius: 10px;
        }

        #userAuctionList .auction-card-info h3 {
            color: #1b2d49;
        }

        #userAuctionList .auction-card-buttons button {
            border-radius: 8px;
            background: linear-gradient(110deg, #1769c2, #2488d4);
        }

        #userAuctionList .auction-card-buttons button:hover {
            background: #1258a8;
        }

        .auction-card-top {
            display: flex;
            gap: 15px;
            align-items: center;
        }

        .auction-card-image {
            width: 110px;
            height: 90px;
            object-fit: cover;
            border-radius: 8px;
            flex-shrink: 0;
        }

        .auction-card-info {
            flex: 1;
        }

        .auction-card-info h3 {
            margin-bottom: 7px;
        }

        .auction-status {
            display: inline-block;
            padding: 4px 8px;
            border-radius: 5px;
            font-size: 12px;
            font-weight: bold;
        }

        .auction-status.waiting {
            background: #e2e3e5;
            color: #41464b;
        }

        .auction-status.running {
            background: #fff3cd;
            color: #856404;
        }

        .auction-status.ended {
            background: #f8d7da;
            color: #842029;
        }

        .auction-card-buttons {
            display: flex;
            gap: 8px;
            margin-top: 12px;
        }

        .auction-card-buttons button {
            margin: 0;
        }

        .admin-auction-card {
            border: 1px solid #ddd;
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 12px;
            background: #f8f9fa;
        }

        .admin-auction-card h4 {
            margin-bottom: 8px;
        }

        .admin-actions {
            display: flex;
            gap: 8px;
            margin-top: 12px;
        }

        .admin-actions button {
            margin: 0;
        }

        .empty-data {
            text-align: center;
            color: #777;
            padding: 25px;
            border: 1px dashed #ccc;
            border-radius: 8px;
        }

        .bidder-analytics {
            margin: 20px 0 26px;
            padding: 20px;
            border: 1px solid #e2eaf4;
            border-radius: 14px;
            background: linear-gradient(145deg, #fbfcff, #f3f7fd);
        }

        .bidder-analytics h4 {
            margin-bottom: 5px;
        }

        .bidder-analytics-intro {
            margin-bottom: 18px;
            color: #6c757d;
            font-size: 0.88rem;
        }

        .bidder-analytics-grid {
            display: grid;
            grid-template-columns: minmax(210px, 0.8fr) minmax(0, 1.6fr);
            gap: 20px;
            align-items: center;
        }

        .bidder-gauge-card {
            display: grid;
            justify-items: center;
            gap: 8px;
            padding: 18px;
            border: 1px solid #e7edf5;
            border-radius: 12px;
            background: white;
        }

        .bidder-gauge {
            position: relative;
            width: 190px;
            height: 105px;
            overflow: hidden;
        }

        .bidder-gauge-arc {
            position: absolute;
            inset: 0 0 auto;
            width: 190px;
            height: 190px;
            border-radius: 50%;
            background: conic-gradient(from 270deg at 50% 50%, #e45d67 0deg, #f3bd4f 54deg, #36b37e 90deg, #edf1f6 90deg 180deg, transparent 180deg);
            -webkit-mask: radial-gradient(circle, transparent 57%, #000 59%);
            mask: radial-gradient(circle, transparent 57%, #000 59%);
            transform: rotate(-90deg);
        }

        .bidder-gauge-needle {
            position: absolute;
            z-index: 1;
            left: 50%;
            bottom: 1px;
            width: 4px;
            height: 73px;
            border-radius: 5px;
            background: #203653;
            transform: translateX(-50%) rotate(-90deg);
            transform-origin: 50% calc(100% - 1px);
            transition: transform 0.5s ease;
        }

        .bidder-gauge-needle::after {
            content: "";
            position: absolute;
            left: 50%;
            bottom: -6px;
            width: 13px;
            height: 13px;
            border-radius: 50%;
            background: #203653;
            transform: translateX(-50%);
        }

        .bidder-gauge-value {
            margin-top: -2px;
            color: #1b2d49;
            font-size: 1.8rem;
            font-weight: 800;
        }

        .bidder-gauge-label {
            color: #758198;
            font-size: 0.84rem;
        }

        .bidder-summary {
            display: grid;
            grid-template-columns: repeat(2, minmax(0, 1fr));
            gap: 12px;
        }

        .bidder-summary-card {
            padding: 16px;
            border: 1px solid #e7edf5;
            border-radius: 11px;
            background: white;
        }

        .bidder-summary-card span {
            display: block;
            margin-bottom: 5px;
            color: #758198;
            font-size: 0.84rem;
        }

        .bidder-summary-card strong {
            color: #1b2d49;
            font-size: 1.45rem;
        }

        .bidder-list-heading {
            display: flex;
            justify-content: space-between;
            align-items: center;
            gap: 12px;
            margin: 22px 0 10px;
        }

        .bidder-list-heading h4 {
            margin: 0;
        }

        .bidder-export-button {
            width: auto;
            margin: 0;
            padding: 10px 14px;
            white-space: nowrap;
        }

        .bidder-table-wrap {
            overflow-x: auto;
        }

        .bidder-table {
            width: 100%;
            min-width: 620px;
            border-collapse: collapse;
            background: white;
        }

        .bidder-table th,
        .bidder-table td {
            padding: 10px;
            border-bottom: 1px solid #e8edf3;
            text-align: left;
            font-size: 0.86rem;
        }

        .bidder-table th {
            color: #43536b;
            background: #f1f5fa;
        }

        .bidder-state {
            display: inline-block;
            padding: 4px 8px;
            border-radius: 20px;
            font-size: 0.78rem;
            font-weight: 700;
        }

        .bidder-state.active {
            color: #0f5132;
            background: #d1e7dd;
        }

        .bidder-state.inactive {
            color: #664d03;
            background: #fff3cd;
        }

        @media(max-width: 600px) {
            .bidder-analytics-grid {
                grid-template-columns: 1fr;
            }

            .bidder-list-heading {
                align-items: stretch;
                flex-direction: column;
            }

            .bidder-export-button {
                width: 100%;
            }
        }

        .winner-results {
            margin: 20px 0 26px;
            padding: 18px;
            border: 1px solid #e2eaf4;
            border-radius: 12px;
            background: #fbfcff;
        }

        .winner-results-heading {
            display: flex;
            align-items: center;
            justify-content: space-between;
            gap: 12px;
            margin-bottom: 12px;
        }

        .winner-results-heading h4 {
            margin: 0 0 4px;
        }

        .winner-results-heading p {
            color: #6c757d;
            font-size: 0.86rem;
        }

        .winner-results-heading button {
            width: auto;
            flex-shrink: 0;
            margin: 0;
            padding: 10px 14px;
        }

        .winner-table-wrap {
            overflow-x: auto;
        }

        .winner-table {
            width: 100%;
            border-collapse: collapse;
            min-width: 680px;
            background: white;
        }

        .winner-table th,
        .winner-table td {
            padding: 11px 10px;
            border-bottom: 1px solid #e8edf3;
            text-align: left;
            font-size: 0.88rem;
            vertical-align: top;
        }

        .winner-table th {
            color: #43536b;
            background: #f1f5fa;
            white-space: nowrap;
        }

        @media(max-width: 600px) {
            .winner-results-heading {
                align-items: flex-start;
                flex-direction: column;
            }

            .winner-results-heading button {
                width: 100%;
            }
        }

        @media(max-width: 600px) {
            body {
                padding: 14px;
            }

            #authSection {
                margin-top: 1vh;
            }

            .home-hero {
                padding: 28px 22px 24px;
            }

            .auth-content {
                padding: 22px;
            }

            .card {
                padding: 20px;
            }

            #authSection {
                padding: 0;
            }

            .auction-card-top {
                align-items: flex-start;
            }

            .auction-card-image {
                width: 90px;
                height: 75px;
            }

            .admin-actions, .admin-tabs, .auth-tabs {
                flex-direction: column;
            }

            .user-topbar {
                padding: 16px 20px;
            }

            .user-dashboard-content {
                padding: 20px 16px 24px;
            }

            .dashboard-hero {
                padding: 24px 20px;
            }

            .hero-emblem {
                flex-basis: 58px;
                width: 58px;
                height: 58px;
                border-radius: 18px;
                font-size: 1.8rem;
            }

            .dashboard-stats {
                grid-template-columns: repeat(2, minmax(0, 1fr));
                gap: 8px;
            }

            .dashboard-stat {
                min-height: 78px;
                flex-direction: column;
                align-items: flex-start;
                gap: 7px;
                padding: 11px;
            }

            .stat-icon {
                display: none;
            }

            .dashboard-stat strong {
                font-size: 1.1rem;
            }

            .dashboard-stat span:last-child {
                font-size: 0.7rem;
            }

            .catalog-heading {
                align-items: flex-start;
            }

            .catalog-label {
                display: none;
            }

            #userAuctionList .auction-card-top {
                flex-direction: column;
            }

            #userAuctionList .auction-card-image {
                width: 100%;
                height: 180px;
            }
        }
    </style>
</head>

<body>

<div class="container">

    <!-- =====================================================
         MODUL AKSES PEMBELI (LOGIN & DAFTAR)
    ====================================================== -->

    <div id="authSection" class="card">
        <header class="home-hero">
            <span class="hero-eyebrow">Lelang online terpercaya</span>
            <h1>Temukan barang pilihan, menangkan penawaran.</h1>
            <p>Ikuti proses lelang yang transparan, pantau harga secara langsung, dan ajukan penawaran dengan mudah.</p>
            <div class="hero-highlights">
                <span>✓ Riwayat bid terbuka</span>
                <span>◷ Waktu lelang real-time</span>
                <span>♙ Akses pembeli mudah</span>
            </div>
        </header>

        <div class="auth-content">
        <div class="auth-tabs">
            <button id="tabLoginBtn" class="active" onclick="switchAuthTab('login')">
                Login Pembeli
            </button>
            <button id="tabRegisterBtn" onclick="switchAuthTab('register')">
                Daftar Akun Baru
            </button>
        </div>

        <!-- FORM LOGIN -->
        <div id="formLogin">
            <h2>Masuk Akun Pembeli</h2>
            <p class="auth-subtitle">Gunakan email terdaftar untuk melihat dan mengikuti lelang yang sedang berlangsung.</p>
            
            <label>Alamat Email Terdaftar</label>
            <input type="email" id="loginEmail" placeholder="Contoh: budi@gmail.com">

            <button onclick="loginUser()">
                Masuk ke Pasar.auction
            </button>
        </div>

        <!-- FORM PENDAFTARAN -->
        <div id="formRegister" class="hidden">
            <h2>Pendaftaran Akun Pembeli</h2>

            <label>Nama Lengkap</label>
            <input type="text" id="regNama" placeholder="Contoh: Budi Santoso" autocomplete="name">

            <label>Nomor Telepon/WA</label>
            <input type="tel" id="regNomor" placeholder="Contoh: 08123456789" autocomplete="tel" inputmode="tel">

            <label>Alamat Email</label>
            <input type="email" id="regEmail" placeholder="Contoh: budi@gmail.com" autocomplete="email">
            <p style="margin:0 0 12px; color:#6b778c; font-size:0.82rem; line-height:1.5;">Gunakan email dan nomor WhatsApp yang dapat dihubungi. Format akan diperiksa sebelum akun dibuat.</p>

            <button onclick="daftarUser()">
                Daftar & Masuk ke Pasar.auction
            </button>
        </div>

        <hr style="margin: 15px 0;">

        <button onclick="showAdminLogin()" class="btn-secondary">
            Masuk sebagai Admin
        </button>
        </div>

    </div>


    <!-- =====================================================
         LOGIN ADMIN
    ====================================================== -->

    <div id="adminLoginSection" class="card hidden">

        <h2>Login Admin</h2>

        <label>Username Admin</label>
        <input type="text" id="adminUser" placeholder="Masukkan Username">

        <label>Kata Sandi</label>
        <input type="password" id="adminPass" placeholder="Masukkan Kata Sandi">

        <button onclick="loginAdmin()" class="btn-success">
            Masuk Admin
        </button>

        <button onclick="showAuthSection()" class="btn-secondary">
            Kembali ke Portal Pembeli
        </button>

    </div>


    <!-- =====================================================
         HALAMAN PEMBELI
    ====================================================== -->

    <div id="userSection" class="card hidden">

        <div class="user-topbar">
            <div class="brand-lockup">
                <span class="brand-mark">◆</span>
                <span>Pasar.auction</span>
            </div>
            <button onclick="logout()" class="btn-danger">
                Keluar
            </button>
        </div>

        <div class="user-dashboard-content">
            <section class="dashboard-hero">
                <div class="dashboard-hero-copy">
                    <span class="dashboard-kicker">Portal pembeli</span>
                    <h1>Selamat datang, <span id="userName"></span>!</h1>
                    <p>Temukan barang pilihan, pantau penawaran secara transparan, dan jadilah pemenang lelang berikutnya.</p>
                </div>
                <div class="hero-emblem" aria-hidden="true">🏆</div>
            </section>

            <div class="dashboard-stats" aria-label="Filter lelang">
                <button type="button" class="dashboard-stat active" data-auction-filter="all" aria-pressed="true" onclick="filterAuctions('all')">
                    <span class="stat-icon" aria-hidden="true">▦</span>
                    <div><strong id="statTotalAuctions">0</strong><span>Total lelang</span></div>
                </button>
                <button type="button" class="dashboard-stat" data-auction-filter="running" aria-pressed="false" onclick="filterAuctions('running')">
                    <span class="stat-icon" aria-hidden="true">◉</span>
                    <div><strong id="statRunningAuctions">0</strong><span>Sedang berlangsung</span></div>
                </button>
                <button type="button" class="dashboard-stat" data-auction-filter="waiting" aria-pressed="false" onclick="filterAuctions('waiting')">
                    <span class="stat-icon" aria-hidden="true">◷</span>
                    <div><strong id="statWaitingAuctions">0</strong><span>Akan dimulai</span></div>
                </button>
                <button type="button" class="dashboard-stat" data-auction-filter="ended" aria-pressed="false" onclick="filterAuctions('ended')">
                    <span class="stat-icon" aria-hidden="true">✓</span>
                    <div><strong id="statEndedAuctions">0</strong><span>Sudah berakhir</span></div>
                </button>
            </div>

            <!-- DAFTAR SEMUA LELANG -->
            <div id="auctionCatalog">
                <div class="catalog-heading">
                    <div>
                        <h2>Jelajahi Lelang</h2>
                        <p>Pilih barang dan ajukan penawaran terbaikmu.</p>
                    </div>
                    <span class="catalog-label">✦ Terbuka untuk semua</span>
                </div>
                <div id="userAuctionList" class="auction-list"></div>
            </div>

        <!-- DETAIL LELANG -->
        <div id="auctionDetail" class="hidden">
            <button onclick="backToAuctionList()" class="btn-secondary">
                ← Kembali ke Daftar Lelang
            </button>
            <br><br>

            <!-- TIMER -->
            <div id="timerDisplay" class="timer-box status-waiting">
                Belum ada barang lelang yang aktif
            </div>

            <!-- PEMENANG -->
            <div id="winnerDisplay" class="winner-box hidden"></div>

            <!-- BARANG -->
            <div id="itemContainer">
                <img id="mainImg" class="main-image" src="https://via.placeholder.com/600x350?text=Belum+Ada+Barang+Lelang" alt="Foto Utama">

                <p style="font-size:0.85em; color:#666; margin-bottom:5px;">
                    Klik foto kecil untuk memperbesar:
                </p>

                <div id="galleryThumbs" class="gallery-thumbs"></div>

                <h3 id="itemName">Belum Ada Barang</h3>
                <p id="itemDescription" style="margin: 0 0 15px; color:#667085; line-height:1.6;"></p>

                <p style="margin-top:5px;">Harga Tertinggi Saat Ini:</p>
                <p class="price" id="highestBid">Rp 0</p>

                <p style="margin-bottom:15px;">
                    Penawar Harga Tertinggi:
                    <strong id="highestBidder" style="color:#0d6efd;">Belum Ada</strong>
                </p>

                <!-- BID -->
                <div id="bidControl" class="hidden">
                    <label>Nominal Penawaran Anda (Rp)</label>
                    <input type="number" id="bidAmount" placeholder="Masukkan nominal lebih tinggi">
                    <button onclick="placeBid()">Kirim Penawaran Terbuka</button>
                </div>
            </div>

            <!-- RIWAYAT BID -->
            <div class="bid-history">
                <h3>Riwayat Penawaran Terbuka</h3>
                <ul id="bidList" class="bid-list"></ul>
            </div>
        </div>
        </div>

    </div>


    <!-- =====================================================
         ADMIN
    ====================================================== -->

    <div id="adminSection" class="card hidden">

        <div style="display:flex; justify-content:space-between; align-items:center; margin-bottom:15px;">
            <h2>Dasbor Admin</h2>
            <button onclick="logout()" class="btn-danger" style="width:auto; padding:6px 12px;">
                Keluar
            </button>
        </div>

        <!-- TAB -->
        <div class="admin-tabs">
            <button id="tabUploadBtn" class="active" onclick="switchAdminTab('upload')">
                1. Upload & Setting Data
            </button>
            <button id="tabMonitorBtn" onclick="switchAdminTab('monitor')">
                2. Monitoring Bidder & Hasil
            </button>
        </div>

        <!-- TAB UPLOAD -->
        <div id="adminTabUpload">
            <h3>Input Barang & Waktu Lelang Baru</h3>

            <label>Nama Barang Lelang</label>
            <input type="text" id="newNamaBarang" placeholder="Contoh: Laptop Gaming ASUS ROG">

            <label>Harga Awal Patokan (Rp)</label>
            <input type="number" id="newHargaAwal" placeholder="Contoh: 5000000">

            <label for="newKeterangan">Keterangan Barang</label>
            <textarea id="newKeterangan" placeholder="Jelaskan kondisi, spesifikasi, atau informasi penting barang"></textarea>

            <label>Upload Foto Barang (Minimal 3 Foto)</label>
            <input type="file" id="uploadFoto" accept="image/*" multiple>
            <p style="font-size:0.8em; color:#d9534f;">* Pilih minimal 3 foto barang.</p>

            <label>Waktu Mulai Lelang</label>
            <input type="datetime-local" id="waktuMulai">

            <label>Waktu Berakhir Lelang</label>
            <input type="datetime-local" id="waktuSelesai">

            <button onclick="updateBarangAdmin()" class="btn-success" style="margin-top:15px;">
                + Simpan & Terbitkan Lelang
            </button>

            <div id="uploadStatus" style="margin-top:10px;"></div>
        </div>

        <!-- TAB MONITORING -->
        <div id="adminTabMonitor" class="hidden">
            <h3>Monitoring Aktivitas Lelang</h3>

            <div style="background:#f8f9fa; padding:15px; border-radius:8px; margin-bottom:15px;">
                <p>Total Lelang: <strong id="totalAuction">0</strong></p>
            </div>

            <section class="bidder-analytics">
                <h4>Aktivitas Akun Bidder · 30 Hari</h4>
                <p class="bidder-analytics-intro">Akun aktif adalah pembeli yang mengajukan bid dalam 30 hari terakhir. Akun tanpa bid dalam periode tersebut dihitung tidak aktif.</p>
                <div class="bidder-analytics-grid">
                    <div class="bidder-gauge-card" role="img" aria-label="Speedometer persentase bidder aktif">
                        <div class="bidder-gauge">
                            <div class="bidder-gauge-arc"></div>
                            <div id="bidderGaugeNeedle" class="bidder-gauge-needle"></div>
                        </div>
                        <strong id="bidderActiveRate" class="bidder-gauge-value">0%</strong>
                        <span class="bidder-gauge-label">persentase bidder aktif</span>
                    </div>
                    <div class="bidder-summary">
                        <div class="bidder-summary-card"><span>Total akun pembeli</span><strong id="bidderTotalCount">0</strong></div>
                        <div class="bidder-summary-card"><span>Aktif · 30 hari</span><strong id="bidderActiveCount">0</strong></div>
                        <div class="bidder-summary-card"><span>Tidak aktif · 30 hari</span><strong id="bidderInactiveCount">0</strong></div>
                        <div class="bidder-summary-card"><span>Periode pemantauan</span><strong style="font-size:1.05rem;">30 hari</strong></div>
                    </div>
                </div>
                <div class="bidder-list-heading">
                    <h4>Daftar Status Bidder</h4>
                    <button onclick="exportAdminReport()" class="btn-success bidder-export-button">Unduh Laporan Excel</button>
                </div>
                <div class="bidder-table-wrap">
                    <table class="bidder-table">
                        <thead><tr><th>Nama</th><th>Status 30 Hari</th><th>Nomor WhatsApp</th><th>Email</th><th>Bid Terakhir</th></tr></thead>
                        <tbody id="adminBidderList"></tbody>
                    </table>
                </div>
            </section>

            <section class="winner-results">
                <div class="winner-results-heading">
                    <div>
                        <h4>Hasil Pemenang Lelang</h4>
                        <p>Nama pemenang, kontak, dan harga final untuk lelang yang telah berakhir.</p>
                    </div>
                    <button onclick="exportTodayWinners()" class="btn-success">Unduh Hasil Hari Ini (.xls)</button>
                </div>
                <div class="winner-table-wrap">
                    <table class="winner-table">
                        <thead>
                            <tr><th>Barang</th><th>Nama Pemenang</th><th>Nomor WhatsApp</th><th>Email</th><th>Harga Final</th><th>Waktu Berakhir</th></tr>
                        </thead>
                        <tbody id="adminWinnerList"></tbody>
                    </table>
                </div>
            </section>

            <h4>Semua Barang Lelang</h4>
            <div id="adminAuctionList" class="auction-list"></div>

            <!-- DETAIL MONITOR -->
            <div id="adminDetail" class="hidden" style="margin-top:20px;">
                <hr>
                <button onclick="backToAdminList()" class="btn-secondary">
                    ← Kembali ke Daftar Lelang
                </button>
                <br><br>

                <h3 id="adminStatusItem">Barang</h3>
                <p id="adminItemDescription" style="margin-bottom:12px; color:#667085; line-height:1.6;"></p>
                <p>Harga Tertinggi / Final: <strong id="adminHargaFinal" style="color:#198754;">Rp 0</strong></p>
                <p>Penawar / Pemenang: <strong id="adminPemenang" style="color:#0d6efd;">Belum Ada</strong></p>

                <h4 style="margin-top:20px;">Aktivitas Semua Penawar</h4>
                <div class="bid-history">
                    <ul id="adminBidList" class="bid-list"></ul>
                </div>

                <button onclick="hapusBarangLelang()" class="btn-danger">
                    Hapus Lelang Ini
                </button>
            </div>
        </div>

    </div>

</div>


<script>

/* ==========================================================
   KONFIGURASI & STORAGE DATA
========================================================== */

const ADMIN_USER = "admin";
const ADMIN_PASS = "admin123";

let currentUser = null;
let registeredUsers = JSON.parse(localStorage.getItem('registeredUsers')) || [];
let daftarLelang = [];
let selectedAuctionId = null;
let timerInterval = null;
let currentAuctionFilter = "all";


/* ==========================================================
   AUTHENTICATION CONTROL (LOGIN / REGISTER SWITCHING)
========================================================== */

function switchAuthTab(tab) {
    const formLogin = document.getElementById("formLogin");
    const formRegister = document.getElementById("formRegister");
    const tabLoginBtn = document.getElementById("tabLoginBtn");
    const tabRegisterBtn = document.getElementById("tabRegisterBtn");

    if (tab === "login") {
        formLogin.classList.remove("hidden");
        formRegister.classList.add("hidden");
        tabLoginBtn.classList.add("active");
        tabRegisterBtn.classList.remove("active");
    } else {
        formLogin.classList.add("hidden");
        formRegister.classList.remove("hidden");
        tabLoginBtn.classList.remove("active");
        tabRegisterBtn.classList.add("active");
    }
}

function showAdminLogin() {
    document.getElementById("authSection").classList.add("hidden");
    document.getElementById("adminLoginSection").classList.remove("hidden");
}

function showAuthSection() {
    document.getElementById("adminLoginSection").classList.add("hidden");
    document.getElementById("authSection").classList.remove("hidden");
}


/* ==========================================================
   LOGIN & PENDAFTARAN PEMBELI
========================================================== */

function loginUser() {
    const emailInput = document.getElementById("loginEmail");
    const email = emailInput ? emailInput.value.trim() : "";

    if (!email) {
        alert("Masukkan alamat email Anda!");
        return;
    }

    const foundUser = registeredUsers.find(u => u.email.toLowerCase() === email.toLowerCase());

    if (foundUser) {
        currentUser = foundUser;
        enterUserSection();
    } else {
        alert("Email belum terdaftar! Silakan pilih tab 'Daftar Akun Baru' terlebih dahulu.");
        switchAuthTab('register');
        document.getElementById("regEmail").value = email;
    }
}

function daftarUser() {
    const nama = document.getElementById("regNama").value.trim();
    const nomorInput = document.getElementById("regNomor").value.trim();
    const email = document.getElementById("regEmail").value.trim().toLowerCase();

    if (!nama || !nomorInput || !email) {
        alert("Harap isi semua data pendaftaran!");
        return;
    }

    if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) {
        alert("Format email belum valid. Periksa kembali alamat email Anda.");
        document.getElementById("regEmail").focus();
        return;
    }

    const digits = nomorInput.replace(/\D/g, "");
    let nomor = digits;
    if (nomor.startsWith("0")) nomor = "62" + nomor.slice(1);
    if (nomor.startsWith("8")) nomor = "62" + nomor;
    if (!/^628\d{8,11}$/.test(nomor)) {
        alert("Masukkan nomor WhatsApp Indonesia yang valid, misalnya 081234567890 atau +6281234567890.");
        document.getElementById("regNomor").focus();
        return;
    }

    const exists = registeredUsers.some(u => u.email.toLowerCase() === email);
    if (exists) {
        alert("Email ini sudah terdaftar. Mengalihkan ke halaman Login...");
        switchAuthTab('login');
        document.getElementById("loginEmail").value = email;
        return;
    }

    currentUser = {
        nama: nama,
        nomor: nomor,
        email: email,
        role: "pembeli"
    };

    registeredUsers.push(currentUser);
    localStorage.setItem('registeredUsers', JSON.stringify(registeredUsers));

    enterUserSection();
}

function enterUserSection() {
    document.getElementById("userName").innerText = currentUser.nama;
    document.getElementById("authSection").classList.add("hidden");
    document.getElementById("userSection").classList.remove("hidden");

    renderUserAuctionList();
    startTimerSystem();
}


/* ==========================================================
   LOGIN ADMIN
========================================================== */

function loginAdmin() {
    const user = document.getElementById("adminUser").value;
    const pass = document.getElementById("adminPass").value;

    if (user === ADMIN_USER && pass === ADMIN_PASS) {
        currentUser = {
            nama: "Administrator",
            role: "admin"
        };

        document.getElementById("adminLoginSection").classList.add("hidden");
        document.getElementById("adminSection").classList.remove("hidden");

        renderAdminAuctionList();
        startTimerSystem();
    } else {
        alert("Username atau Kata Sandi Admin salah!");
    }
}


/* ==========================================================
   TAB ADMIN
========================================================== */

function switchAdminTab(tab) {
    const uploadTab = document.getElementById("adminTabUpload");
    const monitorTab = document.getElementById("adminTabMonitor");
    const uploadBtn = document.getElementById("tabUploadBtn");
    const monitorBtn = document.getElementById("tabMonitorBtn");

    if (tab === "upload") {
        uploadTab.classList.remove("hidden");
        monitorTab.classList.add("hidden");
        uploadBtn.classList.add("active");
        monitorBtn.classList.remove("active");
    } else {
        uploadTab.classList.add("hidden");
        monitorTab.classList.remove("hidden");
        uploadBtn.classList.remove("active");
        monitorBtn.classList.add("active");
        renderAdminAuctionList();
    }
}


/* ==========================================================
   SYSTEM LOGIC & RENDERERS
========================================================== */

function generateAuctionId() {
    return Date.now() + "-" + Math.random().toString(36).substring(2, 9);
}

function updateBarangAdmin() {
    const namaBarang = document.getElementById("newNamaBarang").value.trim();
    const hargaAwal = parseFloat(document.getElementById("newHargaAwal").value);
    const keterangan = document.getElementById("newKeterangan").value.trim();
    const files = document.getElementById("uploadFoto").files;
    const valMulai = document.getElementById("waktuMulai").value;
    const valSelesai = document.getElementById("waktuSelesai").value;

    if (!namaBarang || isNaN(hargaAwal) || !valMulai || !valSelesai) {
        alert("Harap isi seluruh kolom dengan lengkap!");
        return;
    }

    if (files.length < 3) {
        alert("Harap pilih minimal 3 foto barang lelang!");
        return;
    }

    const startTime = new Date(valMulai).getTime();
    const endTime = new Date(valSelesai).getTime();

    if (endTime <= startTime) {
        alert("Waktu berakhir harus lebih lambat dari waktu mulai!");
        return;
    }

    const uploadStatus = document.getElementById("uploadStatus");
    uploadStatus.innerHTML = `<p style="color:#0d6efd;">Sedang memproses ${files.length} foto...</p>`;

    let imageList = [];
    let loadedCount = 0;

    for (let i = 0; i < files.length; i++) {
        const reader = new FileReader();
        reader.onload = function(event) {
            imageList.push(event.target.result);
            loadedCount++;

            if (loadedCount === files.length) {
                const lelangBaru = {
                    id: generateAuctionId(),
                    namaBarang: namaBarang,
                    keterangan: keterangan,
                    hargaAwal: hargaAwal,
                    currentBid: hargaAwal,
                    highestBidderName: "Belum Ada",
                    highestBidderNomor: "",
                    highestBidderEmail: "",
                    imageList: imageList,
                    startTime: startTime,
                    endTime: endTime,
                    bidHistory: [],
                    createdAt: new Date().getTime()
                };

                daftarLelang.push(lelangBaru);

                document.getElementById("newNamaBarang").value = "";
                document.getElementById("newHargaAwal").value = "";
                document.getElementById("newKeterangan").value = "";
                document.getElementById("uploadFoto").value = "";
                document.getElementById("waktuMulai").value = "";
                document.getElementById("waktuSelesai").value = "";

                uploadStatus.innerHTML = `
                    <div style="background:#d1e7dd; color:#0f5132; padding:10px; border-radius:6px;">
                        Lelang berhasil ditambahkan.<br>
                        Total lelang: <strong>${daftarLelang.length}</strong>
                    </div>`;

                renderAdminAuctionList();
            }
        };
        reader.readAsDataURL(files[i]);
    }
}

function getAuctionStatus(auction) {
    const now = new Date().getTime();
    if (now < auction.startTime) return "waiting";
    if (now >= auction.startTime && now <= auction.endTime) return "running";
    return "ended";
}

function getStatusText(status) {
    if (status === "waiting") return "Belum Dimulai";
    if (status === "running") return "Sedang Berlangsung";
    return "Berakhir";
}

function formatRupiah(number) {
    return "Rp " + Number(number).toLocaleString("id-ID");
}

function formatDate(timestamp) {
    return new Date(timestamp).toLocaleString("id-ID", { dateStyle: "medium", timeStyle: "short" });
}

function formatTime(totalSeconds) {
    const hari = Math.floor(totalSeconds / 86400);
    const jam = Math.floor((totalSeconds % 86400) / 3600);
    const menit = Math.floor((totalSeconds % 3600) / 60);
    const detik = totalSeconds % 60;
    return hari + "h " + jam + "j " + menit + "m " + detik + "d";
}

function getRemainingTime(auction) {
    const now = new Date().getTime();
    let target = (now < auction.startTime) ? auction.startTime : auction.endTime;
    const difference = Math.max(0, target - now);
    return formatTime(Math.floor(difference / 1000));
}

function filterAuctions(status) {
    currentAuctionFilter = status;
    document.querySelectorAll("[data-auction-filter]").forEach(button => {
        const isActive = button.dataset.auctionFilter === status;
        button.classList.toggle("active", isActive);
        button.setAttribute("aria-pressed", String(isActive));
    });
    renderUserAuctionList();
}

function renderUserAuctionList() {
    const container = document.getElementById("userAuctionList");
    if (!container) return;

    const counts = {
        all: daftarLelang.length,
        running: daftarLelang.filter(auction => getAuctionStatus(auction) === "running").length,
        waiting: daftarLelang.filter(auction => getAuctionStatus(auction) === "waiting").length,
        ended: daftarLelang.filter(auction => getAuctionStatus(auction) === "ended").length
    };
    document.getElementById("statTotalAuctions").innerText = counts.all;
    document.getElementById("statRunningAuctions").innerText = counts.running;
    document.getElementById("statWaitingAuctions").innerText = counts.waiting;
    document.getElementById("statEndedAuctions").innerText = counts.ended;

    document.querySelectorAll("[data-auction-filter]").forEach(button => {
        const isActive = button.dataset.auctionFilter === currentAuctionFilter;
        button.classList.toggle("active", isActive);
        button.setAttribute("aria-pressed", String(isActive));
    });

    const visibleAuctions = currentAuctionFilter === "all"
        ? daftarLelang
        : daftarLelang.filter(auction => getAuctionStatus(auction) === currentAuctionFilter);

    if (visibleAuctions.length === 0) {
        const emptyMessage = daftarLelang.length === 0
            ? "Belum ada barang lelang."
            : "Belum ada lelang dalam kategori ini.";
        container.innerHTML = `<div class="empty-data">${emptyMessage}</div>`;
        return;
    }

    container.innerHTML = visibleAuctions.map(auction => {
        const status = getAuctionStatus(auction);
        const foto = auction.imageList.length > 0 ? auction.imageList[0] : "https://via.placeholder.com/200";

        return `
            <div class="auction-card">
                <div class="auction-card-top">
                    <img src="${foto}" class="auction-card-image">
                    <div class="auction-card-info">
                        <h3>${escapeHtml(auction.namaBarang)}</h3>
                        <span class="auction-status ${status}">${getStatusText(status)}</span>
                        <p style="margin-top:8px;">Harga Awal: <strong>${formatRupiah(auction.hargaAwal)}</strong></p>
                        <p>Bid Tertinggi: <strong style="color:#198754;">${formatRupiah(auction.currentBid)}</strong></p>
                    </div>
                </div>
                <div style="margin-top:10px; font-size:13px; color:#666;">
                    Sisa waktu: <strong>${getRemainingTime(auction)}</strong>
                </div>
                <div class="auction-card-buttons">
                    <button onclick="openAuction('${auction.id}')" class="btn-success">
                        Lihat & Ikut Lelang
                    </button>
                </div>
            </div>`;
    }).join("");
}

function openAuction(id) {
    const auction = daftarLelang.find(item => item.id === id);
    if (!auction) {
        alert("Data lelang tidak ditemukan.");
        return;
    }

    selectedAuctionId = id;
    document.getElementById("auctionCatalog").classList.add("hidden");
    document.getElementById("auctionDetail").classList.remove("hidden");
    renderSelectedAuction();
}

function renderSelectedAuction() {
    const auction = daftarLelang.find(item => item.id === selectedAuctionId);
    if (!auction) return;

    document.getElementById("itemName").innerText = auction.namaBarang;
    document.getElementById("itemDescription").innerText = auction.keterangan || "Belum ada keterangan untuk barang ini.";
    document.getElementById("highestBid").innerText = formatRupiah(auction.currentBid);
    document.getElementById("highestBidder").innerText = auction.highestBidderName;

    const mainImg = document.getElementById("mainImg");
    const gallery = document.getElementById("galleryThumbs");
    gallery.innerHTML = "";

    if (auction.imageList.length > 0) {
        mainImg.src = auction.imageList[0];
        auction.imageList.forEach((image, index) => {
            const img = document.createElement("img");
            img.src = image;
            img.className = "thumb-img" + (index === 0 ? " active" : "");
            img.onclick = function() {
                mainImg.src = image;
                document.querySelectorAll(".thumb-img").forEach(item => item.classList.remove("active"));
                img.classList.add("active");
            };
            gallery.appendChild(img);
        });
    }

    renderBidHistory();
    updateSelectedAuctionStatus();
}

function updateSelectedAuctionStatus() {
    const auction = daftarLelang.find(item => item.id === selectedAuctionId);
    if (!auction) return;

    const status = getAuctionStatus(auction);
    const timer = document.getElementById("timerDisplay");
    const bidControl = document.getElementById("bidControl");
    const winner = document.getElementById("winnerDisplay");

    if (status === "waiting") {
        timer.className = "timer-box status-waiting";
        timer.innerText = "LELANG BELUM DIMULAI - " + getRemainingTime(auction);
        bidControl.classList.add("hidden");
        winner.classList.add("hidden");
    } else if (status === "running") {
        timer.className = "timer-box status-running";
        timer.innerText = "LELANG BERLANGSUNG! (Sisa: " + getRemainingTime(auction) + ")";
        bidControl.classList.remove("hidden");
        winner.classList.add("hidden");
    } else {
        timer.className = "timer-box status-ended";
        timer.innerText = "BERAKHIR";
        bidControl.classList.add("hidden");
        winner.classList.remove("hidden");

        if (auction.highestBidderName !== "Belum Ada") {
            winner.innerHTML = `🏆 PEMENANG LELANG<br><strong>${escapeHtml(auction.highestBidderName)}</strong><br>Harga Final: <strong>${formatRupiah(auction.currentBid)}</strong>`;
        } else {
            winner.innerHTML = "Lelang Berakhir Tanpa Penawar.";
        }
    }
}

function placeBid() {
    const auction = daftarLelang.find(item => item.id === selectedAuctionId);
    if (!auction) return;

    const status = getAuctionStatus(auction);
    if (status !== "running") {
        alert(status === "waiting" ? "Lelang belum dimulai!" : "Lelang sudah berakhir!");
        return;
    }

    const bid = parseFloat(document.getElementById("bidAmount").value);

    if (isNaN(bid) || bid <= auction.currentBid) {
        alert("Penawaran harus lebih tinggi dari " + formatRupiah(auction.currentBid));
        return;
    }

    auction.currentBid = bid;
    auction.highestBidderName = currentUser.nama;
    auction.highestBidderNomor = currentUser.nomor || "";
    auction.highestBidderEmail = currentUser.email || "";
    auction.bidHistory.unshift({
        nama: currentUser.nama,
        nomor: currentUser.nomor || "",
        email: currentUser.email || "",
        nominal: bid,
        timestamp: Date.now(),
        waktu: new Date().toLocaleString("id-ID")
    });

    document.getElementById("bidAmount").value = "";

    renderSelectedAuction();
    renderUserAuctionList();
    renderAdminAuctionList();
    updateAdminDetail();

    alert("Penawaran berhasil dikirim!");
}

function renderBidHistory() {
    const auction = daftarLelang.find(item => item.id === selectedAuctionId);
    const userList = document.getElementById("bidList");

    if (!auction || auction.bidHistory.length === 0) {
        userList.innerHTML = `<li class="bid-item" style="color:#777; justify-content:center;">Belum ada penawaran.</li>`;
        return;
    }

    userList.innerHTML = auction.bidHistory.map((bid, index) => `
        <li class="bid-item">
            <div>
                <strong>${escapeHtml(bid.nama)}</strong>
                ${index === 0 ? `<span class="badge" style="background:#d1e7dd; color:#0f5132;">Tertinggi</span>` : ""}
                <br><span class="bid-time">${bid.waktu}</span>
            </div>
            <div class="price" style="font-size:1em;">${formatRupiah(bid.nominal)}</div>
        </li>
    `).join("");
}

function getWinnerContact(auction) {
    const latestWinnerBid = auction.bidHistory.find(bid => bid.nama === auction.highestBidderName);
    const registeredWinner = registeredUsers.find(user =>
        (auction.highestBidderEmail && user.email.toLowerCase() === auction.highestBidderEmail.toLowerCase()) ||
        user.nama === auction.highestBidderName
    );

    return {
        nomor: auction.highestBidderNomor || (latestWinnerBid && latestWinnerBid.nomor) || (registeredWinner && registeredWinner.nomor) || "—",
        email: auction.highestBidderEmail || (latestWinnerBid && latestWinnerBid.email) || (registeredWinner && registeredWinner.email) || "—"
    };
}

function isEndedToday(auction) {
    const now = new Date();
    const endDate = new Date(auction.endTime);
    return getAuctionStatus(auction) === "ended" &&
        endDate.getFullYear() === now.getFullYear() &&
        endDate.getMonth() === now.getMonth() &&
        endDate.getDate() === now.getDate();
}

function getTodayWinners() {
    return daftarLelang.filter(auction =>
        isEndedToday(auction) && auction.highestBidderName !== "Belum Ada"
    );
}

function getBidderActivity() {
    const cutoff = Date.now() - 30 * 24 * 60 * 60 * 1000;
    return registeredUsers.map(user => {
        const bids = daftarLelang.flatMap(auction => auction.bidHistory || [])
            .filter(bid => bid.email && user.email && bid.email.toLowerCase() === user.email.toLowerCase())
            .map(bid => ({ ...bid, bidTime: Number(bid.timestamp) || Date.parse(bid.waktu) || 0 }))
            .sort((a, b) => b.bidTime - a.bidTime);
        const lastBidTime = bids.length ? bids[0].bidTime : 0;
        return {
            ...user,
            active: lastBidTime >= cutoff,
            lastBidTime
        };
    });
}

function renderBidderActivity() {
    const list = document.getElementById("adminBidderList");
    if (!list) return;

    const bidders = getBidderActivity();
    const activeCount = bidders.filter(bidder => bidder.active).length;
    const inactiveCount = bidders.length - activeCount;
    const activeRate = bidders.length ? Math.round(activeCount / bidders.length * 100) : 0;

    document.getElementById("bidderTotalCount").innerText = bidders.length;
    document.getElementById("bidderActiveCount").innerText = activeCount;
    document.getElementById("bidderInactiveCount").innerText = inactiveCount;
    document.getElementById("bidderActiveRate").innerText = activeRate + "%";
    document.getElementById("bidderGaugeNeedle").style.transform = `translateX(-50%) rotate(${-90 + activeRate * 1.8}deg)`;

    if (bidders.length === 0) {
        list.innerHTML = `<tr><td colspan="5" style="text-align:center; color:#777;">Belum ada akun pembeli terdaftar.</td></tr>`;
        return;
    }

    list.innerHTML = bidders.map(bidder => `
        <tr>
            <td>${escapeHtml(bidder.nama || "—")}</td>
            <td><span class="bidder-state ${bidder.active ? "active" : "inactive"}">${bidder.active ? "Aktif" : "Tidak aktif"}</span></td>
            <td>${escapeHtml(bidder.nomor || "—")}</td>
            <td>${escapeHtml(bidder.email || "—")}</td>
            <td>${bidder.lastBidTime ? formatDate(bidder.lastBidTime) : "Belum ada bid"}</td>
        </tr>`).join("");
}

function exportAdminReport() {
    const bidders = getBidderActivity();
    const winners = getTodayWinners();
    const bidderRows = bidders.map(bidder => `<tr><td>${escapeHtml(bidder.nama || "—")}</td><td>${bidder.active ? "Aktif" : "Tidak aktif"}</td><td>${escapeHtml(bidder.nomor || "—")}</td><td>${escapeHtml(bidder.email || "—")}</td><td>${bidder.lastBidTime ? formatDate(bidder.lastBidTime) : "Belum ada bid"}</td></tr>`).join("");
    const winnerRows = winners.length
        ? winners.map((auction, index) => {
            const contact = getWinnerContact(auction);
            return `<tr><td>${index + 1}</td><td>${escapeHtml(auction.namaBarang)}</td><td>${escapeHtml(auction.highestBidderName)}</td><td>${escapeHtml(contact.nomor)}</td><td>${escapeHtml(contact.email)}</td><td>${formatRupiah(auction.currentBid)}</td><td>${formatDate(auction.endTime)}</td></tr>`;
        }).join("")
        : `<tr><td colspan="7">Belum ada pemenang dari lelang yang berakhir hari ini.</td></tr>`;

    const content = `\uFEFF<html><head><meta charset="UTF-8"></head><body>
        <h2>Aktivitas Bidder 30 Hari Terakhir</h2>
        <table border="1"><thead><tr><th>Nama</th><th>Status</th><th>Nomor WhatsApp</th><th>Email</th><th>Bid Terakhir</th></tr></thead><tbody>${bidderRows || `<tr><td colspan="5">Belum ada akun pembeli.</td></tr>`}</tbody></table>
        <br><h2>Hasil Pemenang Hari Ini</h2>
        <table border="1"><thead><tr><th>No</th><th>Barang</th><th>Nama Pemenang</th><th>Nomor WhatsApp</th><th>Email</th><th>Harga Final</th><th>Waktu Berakhir</th></tr></thead><tbody>${winnerRows}</tbody></table>
        </body></html>`;
    const blob = new Blob([content], { type: "application/vnd.ms-excel;charset=utf-8" });
    const url = URL.createObjectURL(blob);
    const link = document.createElement("a");
    const now = new Date();
    const dateStamp = `${now.getFullYear()}-${String(now.getMonth() + 1).padStart(2, "0")}-${String(now.getDate()).padStart(2, "0")}`;
    link.href = url;
    link.download = `laporan-bidder-dan-pemenang-${dateStamp}.xls`;
    document.body.appendChild(link);
    link.click();
    link.remove();
    URL.revokeObjectURL(url);
}

function renderWinnerResults() {
    const list = document.getElementById("adminWinnerList");
    if (!list) return;

    const endedAuctions = daftarLelang.filter(auction => getAuctionStatus(auction) === "ended");
    if (endedAuctions.length === 0) {
        list.innerHTML = `<tr><td colspan="6" style="text-align:center; color:#777;">Belum ada lelang yang berakhir.</td></tr>`;
        return;
    }

    list.innerHTML = endedAuctions.map(auction => {
        const hasWinner = auction.highestBidderName !== "Belum Ada";
        const contact = hasWinner ? getWinnerContact(auction) : { nomor: "—", email: "—" };
        return `<tr>
            <td>${escapeHtml(auction.namaBarang)}</td>
            <td>${escapeHtml(auction.highestBidderName)}</td>
            <td>${escapeHtml(contact.nomor)}</td>
            <td>${escapeHtml(contact.email)}</td>
            <td>${hasWinner ? formatRupiah(auction.currentBid) : "—"}</td>
            <td>${formatDate(auction.endTime)}</td>
        </tr>`;
    }).join("");
}

function exportTodayWinners() {
    const winners = getTodayWinners();
    if (winners.length === 0) {
        alert("Belum ada hasil pemenang lelang yang berakhir hari ini.");
        return;
    }

    const rows = winners.map((auction, index) => {
        const contact = getWinnerContact(auction);
        return `<tr><td>${index + 1}</td><td>${escapeHtml(auction.namaBarang)}</td><td>${escapeHtml(auction.highestBidderName)}</td><td>${escapeHtml(contact.nomor)}</td><td>${escapeHtml(contact.email)}</td><td>${formatRupiah(auction.currentBid)}</td><td>${formatDate(auction.endTime)}</td></tr>`;
    }).join("");

    const excelContent = `\uFEFF<html><head><meta charset="UTF-8"></head><body><table border="1"><thead><tr><th>No</th><th>Barang</th><th>Nama Pemenang</th><th>Nomor WhatsApp</th><th>Email</th><th>Harga Final</th><th>Waktu Berakhir</th></tr></thead><tbody>${rows}</tbody></table></body></html>`;
    const blob = new Blob([excelContent], { type: "application/vnd.ms-excel;charset=utf-8" });
    const url = URL.createObjectURL(blob);
    const link = document.createElement("a");
    const now = new Date();
    const dateStamp = `${now.getFullYear()}-${String(now.getMonth() + 1).padStart(2, "0")}-${String(now.getDate()).padStart(2, "0")}`;
    link.href = url;
    link.download = `hasil-pemenang-lelang-${dateStamp}.xls`;
    document.body.appendChild(link);
    link.click();
    link.remove();
    URL.revokeObjectURL(url);
}

function renderAdminAuctionList() {
    const container = document.getElementById("adminAuctionList");
    if (!container) return;

    document.getElementById("totalAuction").innerText = daftarLelang.length;
    renderWinnerResults();
    renderBidderActivity();

    if (daftarLelang.length === 0) {
        container.innerHTML = `<div class="empty-data">Belum ada barang lelang.</div>`;
        return;
    }

    container.innerHTML = daftarLelang.map((auction, index) => {
        const status = getAuctionStatus(auction);
        const foto = auction.imageList.length ? auction.imageList[0] : "";

        return `
            <div class="admin-auction-card">
                <div style="display:flex; gap:15px;">
                    <img src="${foto}" style="width:100px; height:80px; object-fit:cover; border-radius:7px;">
                    <div>
                        <h4>#${index + 1} - ${escapeHtml(auction.namaBarang)}</h4>
                        <span class="auction-status ${status}">${getStatusText(status)}</span>
                        <p style="margin-top:8px;">Harga: <strong>${formatRupiah(auction.currentBid)}</strong></p>
                        <p>Bidder: <strong>${escapeHtml(auction.highestBidderName)}</strong></p>
                    </div>
                </div>
                <p style="margin-top:10px; color:#666; font-size:13px;">
                    Mulai: ${formatDate(auction.startTime)}<br>
                    Selesai: ${formatDate(auction.endTime)}
                </p>
                <div class="admin-actions">
                    <button onclick="monitorAuction('${auction.id}')" class="btn-success">Monitoring</button>
                    <button onclick="hapusAuction('${auction.id}')" class="btn-danger">Hapus</button>
                </div>
            </div>`;
    }).join("");
}

function monitorAuction(id) {
    selectedAuctionId = id;
    document.getElementById("adminAuctionList").classList.add("hidden");
    document.getElementById("adminDetail").classList.remove("hidden");
    updateAdminDetail();
}

function updateAdminDetail() {
    const auction = daftarLelang.find(item => item.id === selectedAuctionId);
    if (!auction) return;

    document.getElementById("adminStatusItem").innerText = auction.namaBarang;
    document.getElementById("adminItemDescription").innerText = auction.keterangan || "Belum ada keterangan untuk barang ini.";
    document.getElementById("adminHargaFinal").innerText = formatRupiah(auction.currentBid);
    document.getElementById("adminPemenang").innerText = auction.highestBidderName;

    const list = document.getElementById("adminBidList");
    if (auction.bidHistory.length === 0) {
        list.innerHTML = `<li class="bid-item" style="color:#777; justify-content:center;">Belum ada aktivitas penawaran.</li>`;
        return;
    }

    list.innerHTML = auction.bidHistory.map((bid, index) => `
        <li class="bid-item">
            <div>
                <strong>${escapeHtml(bid.nama)}</strong>
                ${index === 0 ? `<span class="badge">Bid Tertinggi</span>` : ""}
                <br><span class="bid-time">${bid.waktu}</span>
            </div>
            <div class="price" style="font-size:1em;">${formatRupiah(bid.nominal)}</div>
        </li>
    `).join("");
}

function backToAdminList() {
    document.getElementById("adminDetail").classList.add("hidden");
    document.getElementById("adminAuctionList").classList.remove("hidden");
    selectedAuctionId = null;
    renderAdminAuctionList();
}

function hapusAuction(id) {
    const auction = daftarLelang.find(item => item.id === id);
    if (!auction || !confirm("Hapus lelang " + auction.namaBarang + "?")) return;

    daftarLelang = daftarLelang.filter(item => item.id !== id);
    if (selectedAuctionId === id) selectedAuctionId = null;

    renderAdminAuctionList();
    renderUserAuctionList();
}

function hapusBarangLelang() {
    if (!selectedAuctionId) return;
    hapusAuction(selectedAuctionId);
    backToAdminList();
}

function backToAuctionList() {
    selectedAuctionId = null;
    document.getElementById("auctionDetail").classList.add("hidden");
    document.getElementById("auctionCatalog").classList.remove("hidden");
    renderUserAuctionList();
}

function startTimerSystem() {
    if (timerInterval) clearInterval(timerInterval);
    timerInterval = setInterval(function() {
        renderUserAuctionList();
        renderWinnerResults();
        updateSelectedAuctionStatus();
        updateAdminTimer();
    }, 1000);
}

function updateAdminTimer() {
    if (!selectedAuctionId) return;
    const detail = document.getElementById("adminDetail");
    if (detail.classList.contains("hidden")) return;
    updateAdminDetail();
}

function escapeHtml(text) {
    return String(text)
        .replace(/&/g, "&amp;")
        .replace(/</g, "&lt;")
        .replace(/>/g, "&gt;")
        .replace(/"/g, "&quot;")
        .replace(/'/g, "&#039;");
}

function logout() {
    currentUser = null;
    selectedAuctionId = null;

    document.getElementById("userSection").classList.add("hidden");
    document.getElementById("adminSection").classList.add("hidden");
    document.getElementById("adminLoginSection").classList.add("hidden");
    document.getElementById("authSection").classList.remove("hidden");

    document.getElementById("loginEmail").value = "";
    document.getElementById("regNama").value = "";
    document.getElementById("regNomor").value = "";
    document.getElementById("regEmail").value = "";
    document.getElementById("adminUser").value = "";
    document.getElementById("adminPass").value = "";
}

</script>

</body>
</html>
