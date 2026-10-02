# Database: ruang_pribadi

## Table: dim_stocks

| Column | Type | Null | Key | Default | Extra |
|--------|------|------|-----|---------|-------|
| ticker | varchar(10) | NO | PRI | NULL | |
| company_name | varchar(200) | YES | | NULL | |
| label_delisted | tinyint(4) | YES | MUL | NULL | |
| Sector | varchar(100) | YES | | NULL | |
| Primary_Sector | varchar(100) | YES | | NULL | |
| Sub_Sector | varchar(100) | YES | | NULL | |
| Core_Business_Product_Service | text | YES | | NULL | |

### Sample Data (dim_stocks)

| ticker | company_name | label_delisted | Sector | Primary_Sector | Sub_Sector | Core_Business_Product_Service |
|--------|--------------|----------------|--------|----------------|------------|-------------------------------|
| AADI | Adaro Andalan Indonesia Tbk. | 0 | Energi | Pertambangan | Batubara | Menambang dan menjual batu bara termal serta menyediakan jasa penunjang pertambangan sebagai bagian dari Grup Adaro. |
| AALI | Astra Agro Lestari Tbk. | 0 | Konsumen Primer | Agribisnis | Perkebunan Kelapa Sawit | Mengelola perkebunan kelapa sawit dan memproduksi CPO, inti sawit, serta produk turunan oleokimia. |
| ABBA | Mahaka Media Tbk. | 0 | Teknologi | Media & Hiburan Digital | Penerbitan & Media Cetak/Digital | Menerbitkan surat kabar Republika, majalah Golf Digest, serta mengelola platform media digital dan periklanan. |

## Table: fact_daily_summary

| Column | Type | Null | Key | Default | Extra |
|--------|------|------|-----|---------|-------|
| trade_date | date | NO | PRI | NULL | |
| row_no | int(11) | YES | | NULL | |
| ticker | varchar(10) | NO | PRI | NULL | |
| remarks | varchar(50) | YES | | NULL | |
| prev_price | double | YES | | NULL | |
| open_price | double | YES | | NULL | |
| last_trading_date | varchar(20) | YES | | NULL | |
| first_trade | double | YES | | NULL | |
| high | double | YES | | NULL | |
| low | double | YES | | NULL | |
| close | double | YES | | NULL | |
| change | double | YES | | NULL | |
| volume | bigint(20) | YES | | NULL | |
| value | double | YES | | NULL | |
| frequency | int(11) | YES | | NULL | |
| individual_index | double | YES | | NULL | |
| offer | double | YES | | NULL | |
| offer_volume | bigint(20) | YES | | NULL | |
| bid | double | YES | | NULL | |
| bid_volume | bigint(20) | YES | | NULL | |
| listed_shares | bigint(20) | YES | | NULL | |
| tradable_shares | bigint(20) | YES | | NULL | |
| weight_for_index | int(11) | YES | | NULL | |
| foreign_sell | bigint(20) | YES | | NULL | |
| foreign_buy | bigint(20) | YES | | NULL | |
| non_reg_volume | bigint(20) | YES | | NULL | |
| non_reg_value | double | YES | | NULL | |
| non_reg_freq | int(11) | YES | | NULL | |

### Sample Data (fact_daily_summary)

| trade_date | row_no | ticker | remarks | prev_price | open_price | last_trading_date | first_trade | high | low | close | change | volume | value | frequency | individual_index | offer | offer_volume | bid | bid_volume | listed_shares | tradable_shares | weight_for_index | foreign_sell | foreign_buy | non_reg_volume | non_reg_value | non_reg_freq |
|------------|--------|--------|---------|------------|------------|-------------------|-------------|------|-----|-------|--------|--------|-------|-----------|------------------|-------|--------------|-----|------------|---------------|-----------------|------------------|--------------|-------------|----------------|----------------|--------------|
| 2020-01-02 | 1 | AALI | --S1K--1 | 14575 | 0 | 02 Jan 2020 | 0 | NULL | NULL | 14025 | -550 | 799000 | 11451335000 | 888 | NULL | 14200 | 12200 | 14025 | 49900 | 1924688333 | 1924688333 | 1924688333 | 106300 | 253800 | 0 | 0 | 0 |
| 2020-01-02 | 2 | ABBA | --U9---2 | 106 | 0 | 02 Jan 2020 | 0 | NULL | NULL | 105 | -1 | 6340800 | 671926200 | 624 | NULL | 106 | 201200 | 105 | 786900 | 2755125000 | 2755125000 | 2147483647 | 21600 | 0 | 0 | 0 | 0 |
| 2020-01-02 | 3 | ABDA | --U8---2 | 6975 | 0 | 02 Jan 2020 | 0 | NULL | NULL | 6925 | -50 | 1700 | 12012500 | 6 | NULL | 6775 | 100 | 5600 | 100 | 620806680 | 620806680 | 620806680 | 1600 | 0 | 0 | 0 | 0 |
