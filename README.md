import time
import socket
import threading
import select
import re
import requests
import random
from datetime import datetime
lag_status = False
global roomretst
roomretst = False
gameplayed= 0
serversocket =None
remotesockett = None
clienttsocket =None
istarted = False
start =None
increase =False
socktion =None
SOCKS_VERSION = 5
packet =b''
defult_value = 000000000000000000000000000000000
full = False
one = True

SERVER_HOST = '140.150.224.42'
SERVER_PORT = 10033
client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
client.connect((SERVER_HOST, SERVER_PORT))
global command
command = False

def command_bot(value42w):
    global command
    command = value42w
    return command

global add_yout
add_yout = False

def youtubers(value42):
    global add_yout
    add_yout = value42
    return add_yout

def start_des(tar,five):
    five.send(bytes.fromhex("0f1500000010"+EncryptFF(f"080112090a05{tar}1001")))
    threading.Thread(target=destroy).start()

def inv_ent(tat_id):
    pay = f"080112090a05{tat_id}1001"
    new_pay = "0f1500000010"+EncryptFF(pay)
    five.send(bytes.fromhex(new_pay))
    threading.Thread(target=enter_to).start()

def enter_to_game(enc_client_id):
    pay = f"080112090a05{enc_client_id}1001"
    new_pay = "0f1500000010"+EncryptFF(pay)
    five.send(bytes.fromhex(new_pay))
    threading.Thread(target=start_game).start()

def player_info(p_id,getin,newdataS2):
    print("Sending info")
    getin.send(bytes.fromhex(gen_msgv2_clan(f"[00FF00][b][c]جـلـب مـعـلـومـات الحساب ..",newdataS2)))
    getin.send(bytes.fromhex(gen_msgv2_clan(f"[4dd0e1][b][c]الأيدي : ",newdataS2)))
    getin.send(bytes.fromhex(gen_msgv2_clan(f"[ff5722][b][c]{p_id}",newdataS2)))
    getin.send(bytes.fromhex(gen_msgv2_clan(f"[4dd0e1][b][c]الإسـم : ",newdataS2)))
    getin.send(bytes.fromhex(gen_msgv2_clan(f"[ff5722][b][c]{getname(p_id)}",newdataS2)))
    getin.send(bytes.fromhex(gen_msgv2_clan(f"[4dd0e1][b][c]السيرفـر : ",newdataS2)))
    getin.send(bytes.fromhex(gen_msgv2_clan(f"[ff5722][b][c]{getreg(p_id)}",newdataS2)))
    getin.send(bytes.fromhex(gen_msgv2_clan(f"[4dd0e1][b][c]حالـة الحسـاب : ",newdataS2)))
    getin.send(bytes.fromhex(gen_msgv2_clan(f"[ff5722][b][c]{get_status(p_id)}",newdataS2)))
    getin.send(bytes.fromhex(gen_msgv2_clan(f"[76ff03][b][c] تـاريخ الإنشـاء : ",newdataS2)))
    getin.send(bytes.fromhex(gen_msgv2_clan(f"{getdate(p_id)}",newdataS2)))

def fake_frind(target_id,cw):
    BNS = ["b2dd8dae03","b1dd8dae03","bfdc8dae03"]
    probabilities = [3.3333, 3.3333, 3.3333]
    B_N = random.choices(BNS, probabilities)[0]
    if len(target_id) == 8:
        cw.send(bytes.fromhex(f"060000007708d4d7faba1d100620022a6b08{target_id}1a1b5b3030666666665d42595445202020424f542e5b3030666666665d32024d454049b00101b801e807d801d4d8d0ad03e001{B_N}ea011eefbca8efbca5efbcb2efbcafefbcb3efbca8efbca9efbcadefbca1efa3bf8002fd98a8dd03900201d00201"))

    if len(target_id) > 8:
        print("Add Frind")
        cw.send(bytes.fromhex(f"060000006808d4d7faba1d100620022a5c08{target_id}1a1b5b3030464646465d42595445e385a4424f542e5b3030464646465d32024d45404db00113b801a528d801d4d8d0ad03e001{B_N}f00101f8019a018002fd98a8dd03900201d0020cd8022ee002b2e9f7b103"))


def g5(enc_client_id,cw,five,cli,dat):
    cli.send(bytes.fromhex(gen_msgv2_clan(f"[304ffe][b][c]  فـــــريــــــق  5  <--",dat)))
    cw.send(bytes.fromhex(f"050000027108{enc_client_id}100520122ae40408{enc_client_id}12024d4518012004328e0408{enc_client_id}1211534849524fe385a4485550e385a4efa3bf1a024d4520b6f3d7a6062841308bcbd13038324214e99fe061e8b6ce64a6a3e860c3b5ce64d79ba3614801500158e80768c6dd8dae037a058990c5b00382012408dbdaf1eb04120ad8a7d984d988d8add8b4180720df87d4f0042a0808cb9d85f304100388019dffc4b00392010e010407090a0b120f16191a1e2023980101a801d288f8b103c00101c80101e80106f00112880203920208b609ca13b917f923aa0207080110e7592001aa0208080210963318dc0baa0206080f10a09c01aa0205081710894faa0205081810de3caa0205081a10ba40aa0205081b10b237aa0205081c10b247aa02050820109749aa0205082210ee40aa0205082310a845aa0205082b10cb41aa0206083910fa9801aa0206083d10829c01aa0208084910803218dc0baa0205084d10e432aa0206082110a09c01aa0205083110cb41aa0206084110a09c01aa0206083410a09c01aa0205082810e432aa0205082910e432c2021712041a0201041a0208501a090848120501040506072200ca020e0804106d1858200128f0c0e5a606d00205ea02520a4c68747470733a2f2f67726170682e66616365626f6f6b2e636f6d2f76392e302f3534333935303432363130353731322f706963747572653f77696474683d313630266865696768743d31363010011801f2020082030b08f8ddcab0032a03108d018a03003a011a403e50056801721e313639313734343639343831393738363933335f3730666e736b733666717801820103303b30880181e08bc5b9d3f4b917a20100a80101b00114"))
    gg = EncryptFF(f"0811121a08{enc_client_id}10011804203e2a011a400548015203303b306814")
    five.send(bytes.fromhex("051500000020"+gg))

def visible_ent(target_id):
    if len(number) == 10:
        py_packet = EncryptFF(f"082112e10408{target_id}12024d45180220092a0e010407090a0b120f16191a1e20233211534849524fe385a4485550e385a4efa3bf380140e8074864520245475a203734323862323533646566633136343031386336303461316562626665626466600168{target_id}8001018a0187030a8001303946464233424632344334453135443032303638363035353535353030303030313130303030323031304530303631313933333134343530383435313434353431373432323134313130313033326137383566643433313831653964623062363463386431366530303030303066663261326531363031346636356161623610bc0a1add017650545212074e735e594b507f697a43077a7e0f5a6f635e515d61730d7e546352450a120845694156594054637c5d7f64404f737a06587b406247510163465b090514024a035365747b0e7657417c024241604f434b63557c4972715d017e7f0f14034c6f5c0250075a501e475a7355634c057575076859447f0645447247041b0e4d4056435c637f6f6e055c6a7901660a0b00764501547f690f7507600b11024d550c7b045e7f53555e764a404f500f7046597177795b6b607542090d1a0c4b670e676d70436848604354795540430f76446b04006d69006b7e620c22047757595430073a0a1571607a5071787f13154207312e3130302e3348035002900101a201080a04494443311065ba01520a4c68747470733a2f2f67726170682e66616365626f6f6b2e636f6d2f76392e302f3534333935303432363130353731322f706963747572653f77696474683d313630266865696768743d31363010011801c001c6dd8dae03d20100")
        five.send(bytes.fromhex("051500000270"+py_packet))

    if len(number) == 9:
        py_packet = EncryptFF(f"082112e60408{target_id}12024d45180220092a0e010407090a0b120f16191a1e2023320f42595445e385a4424f54e385a45633380140e8074864520245475a203734323862323533646566633136343031386336303461316562626665626466600168{target_id}8001018a0185030a8001303946454233424545334630343230363032303339303035353535353030303030313131303030323031304630303637313336423139363330393633313936333431373432323134313130313033326637383566643433313831653964623062363463386431366530303030303066663264333131383031653466396562313110fb0e1add0177515b5d11024f75575843507f607e42037a760753606550515963720c77526a534f0f100b4d69475657455b607f57766b4048797a0f5a714b644e56026c4053020e10024400556c737a04725546760442496e4f4649665673497370520e7d7a0e120a4d675c0259035b541e4f527a5a65420571770669504276074f4170440c1b084d4e534c5f60756661055b607908640000067f42025b7961047e036005120444520d71005c7859535e7e44404a520a7349597076765468657444000c120c4b6e0a6669704b60416f455a795142420e7f4262050a686b03637e640c22047f575f5430073a081c617f747b6115154207312e3130302e3348035002900101a201080a04494443311053ba01600a5a68747470733a2f2f6c68332e676f6f676c6575736572636f6e74656e742e636f6d2f612f414163485474644e756868595a377936422d5a45726b77536d686758383651626b4170316f53414b31384e376c5836423d7339362d6310011801d201020801")
        five.send(bytes.fromhex("051500000270"+py_packet))


    if len(number) == 8:
        py_packet = EncryptFF(f"082112ee0408{target_id}12024d45180220092a0e010407090a0b120f16191a1e2023320e4d4f48414d4544e385a4425954453801408b084864520245475a203734323862323533646566633136343031386336303461316562626665626466600168e8bbf3ea028001018a0186030a8001303946464233424543373343423846323032303231363031313131313030303030303636303030323030363430303045303332463336383030383830333638303431373432323134313130313033303637383566643433313831653964623062363463386431366530303030303066663036303630343031653463326635653910f9021add01705e555411024e71595a445f71697e42027e7805546f6b5951596276027555655d460f100a49674551584b52607f567265424f7674065a714a60405405634e5a020e11064a0252637d7304725442780645466046464967527d4b747f5c077d7a0f16044f60530c50035b551a41507d556b4b0571760267524579094641704508150a4a415d455f6074626f075c6f770164000102714005547768047e02640b10034b5c0471005d7c575159714a494a520b77475b7779785d686575400e0e150345670a666874456246604b5379514346007d456d0b03686b026770660b22047b595d5330073a091d7c710067066617124207312e3130302e3348035002900103980106a201090a044944433110ac02ba01600a5a68747470733a2f2f6c68332e676f6f676c6575736572636f6e74656e742e636f6d2f612f4141634854746372366e6753636c6d446839554d4c7878374c67725a387235555333594258357936316a4437686c4e5a3d7339362d6310011801c001a7f48fae03d20100")
        five.send(bytes.fromhex("051500000280"+py_packet))


def sendi():
    global snv,dataC
    while True:
        if '0515' in dataC.hex()[0:4] and len(dataC.hex()) >= 900:
            for i in range(400):
                snv.send(dataC)
                for k in range(1):
                    time.sleep(0.001)

            break

def start_game():
    global dataS
    for i in range(200):
        if "0f00" in dataS.hex():
            pattern = r'40(.{8,12})80'
            matches = re.findall(pattern, dataS.hex())
            print(matches)
            for match in matches:
                    target_id5 = match[:-1]
                    five.send(bytes.fromhex(("051500000010"+EncryptFF(f"0809120608{target_id5}"))))
            break
        print("No id")
        time.sleep(0.1)

def runsnv():
    threading.Thread(target=sendi).start()
    threading.Thread(target=sendi).start()

def enter_to():
    global dataS
    global five
    global cw
    global enc_client_id
    while True:
        if '0f00' in dataS.hex()[:4] and len(dataS.hex()) < 120:
            print("yes")
            pattern = r'40(.{8,12})80'
            matches = re.findall(pattern, dataS.hex())
            for match in matches:
                    print(match[:-1])
                    target_id2 = match[:-1]
                    print("Enter SQuad")


                    ent_packet = f"050000049e08{enc_client_id}100520062a910908{target_id2}12024d4518012003328b0508{target_id2}120e4d4f48414d4544e385a4425954451a024d4520a4d1d5a606281e30a7cbd13038324218c091e660c0b5ce648096a36180c3856680a89763c09ae06148015001588b0868a7f48fae0382011808d1daf1eb04180420d487d4f0042a0808c79d85f304100392010c0107090a0b120f16191a1e20980103a00106c00101c80101e80101fa010808021006180f2859fa010a08021006180f20012859fa010a08021006180f20032859fa010a08021006180f20042859fa010808021009181b2859fa010a08021009181b20012859fa010a08021009181b20032859fa010a08021009181b20042859fa010808021001181b2859fa010a08021001181b20012859fa010a08021001181b20032859fa010a08021001181b20042859fa010a08021002180120012859fa010a08021002180120032859fa0108080210021801284f880208920208ae2dce01c205ee07aa0208080110e43218807daa0208080f10ad3218904eaa0205081710e432aa0205082b10d832aa0205080210e432aa0205081810ad32aa0205081a10ad32aa0205081c10ad32aa0205082010ad32aa0205082210ad32aa0205082110ad32aa0205082310ad32aa0205083110d832aa0205083910ad32aa0205083d10ad32aa0205084110ad32aa0205084910d836aa0205084d10e432aa0205081b10ad32aa0205083410ad32aa0205082810e432aa0205082910e432c2021712041a0201041a090848120501040506071a0208502200ea02600a5a68747470733a2f2f6c68332e676f6f676c6575736572636f6e74656e742e636f6d2f612f4141634854746372366e6753636c6d446839554d4c7878374c67725a387235555333594258357936316a4437686c4e5a3d7339362d6310011801f202008a030032a70308{enc_client_id}120f42595445e385a4424f54e385a456331a024d4520b2d1d5a60628013085cbd13038324218c091e66080a89763c0b5ce64c09ae0618096a36180c385664801500158e80792010c0107090a0b120f16191a1e20980101c00101c80101e801018802089202029603aa0208080110e43218807daa0209080f10e43218f0ab01aa0205080210e432aa0205081810e432aa0205081a10e432aa0205081c10e432aa0205082010e432aa0205082210e432aa0205082110e432aa0205081710e432aa0205082310e432aa0205082b10e432aa0205083110e432aa0205083910e432aa0205083d10e432aa0205084110e432aa0205084910d836aa0205084d10e432aa0205081b10e432aa0205083410e432aa0205082810e432aa0205082910e432c2021712041a0201041a090848120501040506071a0208502200ea02600a5a68747470733a2f2f6c68332e676f6f676c6575736572636f6e74656e742e636f6d2f612f414163485474644e756868595a377936422d5a45726b77536d686758383651626b4170316f53414b31384e376c5836423d7339362d63100118018a030208013a020116400150015a07313232323530346801721e313639313730373535363633303138323130315f7937667a72376d306a62880180e08babfd9dd1b917a20100b00114ea010449444331"
                    cw.send(bytes.fromhex(ent_packet))
                    five.send(b'\x05\x03\x00\x00')
                    
            break
##############################################

def sayhello():
    client.send("12345678".encode())
    response = client.recv(999999)

def convert_id(p_id):
    client.send(p_id.encode())
    response = client.recv(999999)
    return response.decode()
    

def EncryptFF(packet):
    client.send(bytes.fromhex(packet))
    response = client.recv(999999)
    return response.hex()

##############################################
def lag_sqqq(five,target_id):
    global enc_client_id
    if len(target_id) == 8:
    
        newpaa = "0515000000a0"+EncryptFF(f"083d12980108e8bbf3ea02128f0108{target_id}10{enc_client_id}1a0e4d4f48414d4544e385a44259544520a7f48fae0328ca88daa606303e381a42600a5a68747470733a2f2f6c68332e676f6f676c6575736572636f6e74656e742e636f6d2f612f4141634854746372366e6753636c6d446839554d4c7878374c67725a387235555333594258357936316a4437686c4e5a3d7339362d63100118014805")
    if len(target_id) != 8:

        paa = f"083d12990108{target_id}12900108{target_id}10d3b1b0b91c1a0e4d4f48414d4544e385a44259544520a7f48fae032899f8d6a606303e381a42600a5a68747470733a2f2f6c68332e676f6f676c6575736572636f6e74656e742e636f6d2f612f4141634854746372366e6753636c6d446839554d4c7878374c67725a387235555333594258357936316a4437686c4e5a3d7339362d63100118014805"
        newpaa = "0515000000a0"+EncryptFF(paa)
    global lag_status
    for i in range(2000):
        if lag_status == False:
            break
        five.send(bytes.fromhex(newpaa))
        for l in range(1):
            time.sleep(0.005)
            print(f"lag{i}")


def destroy():
    global dataS
    global five
    print("i'm Here")
    while True:
        if '0f00' in dataS.hex()[:4]:
            print("yes")
            pattern = r'40(.{8,12})80'
            matches = re.findall(pattern, dataS.hex())
            print(matches)
            for match in matches:
                    print(match[:-1])
                    target_id2 = match[:-1]
                    print(target_id2)
                    threading.Thread(target=lag_sqqq,args=(five,target_id2)).start()
            break

def getdate(playerid):
    global data, dc
    try:
        data = requests.get(f"http://88.198.53.59:19350/info/{playerid}").json()
        dc = data["date"]
        print(dc)
        
        old_date = datetime.strptime(dc, "%d/%m/%Y")
        now = datetime.now()
        delta = now - old_date
        years = delta.days // 365
        months = (delta.days % 365) // 30
        days = (delta.days % 365) % 30
        return f"[b][c][ffea00]{dc}\n\n[18ffff]{years} سنوات \n\n{months} شهور \n\n{days} يوم "
    except:
        return f"[b][c][ffea00]{dc}"
    
def getreg(Id):    
     
    url = "https://shop2game.com/api/auth/player_id_login"
    headers = {
        "Accept": "application/json",
        "Accept-Encoding": "gzip, deflate, br",
        "Accept-Language": "en-US,en;q=0.9,en;q=0.8",
        "Content-Type": "application/json",
        "Origin": "https://shop2game.com",
        "Referer": "https://shop2game.com/app",
        "sec-ch-ua": '"Google Chrome";v="111", "Not(A:Brand";v="8", "Chromium";v="111"',
        "sec-ch-ua-mobile": "?0",
        "sec-ch-ua-platform": "Windows",
        "Sec-Fetch-Dest": "empty",
        "Sec-Fetch-Mode": "cors",
        "Sec-Fetch-Site": "same-origin",
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/111.0.0.0 Safari/537.36",
        "x-datadome-clientid": "10BIK2pOeN3Cw42~iX48rEAd2OmRt6MZDJQsEeK5uMirIKyTLO2bV5Ku6~7pJl_3QOmDkJoSzDcAdCAC8J5WRG_fpqrU7crOEq0~_5oqbgJIuVFWkbuUPD~lUpzSweEa",
    }
    payload = {
        "app_id": 100067,
        "login_id": f"{Id}",
        "app_server_id": 0,
    }
    response = requests.post(url, headers=headers, json=payload)
    try:
        if response.status_code == 200:
            return response.json()['region']
        else:
            return(f"ERROR")
    except:
        return("السيرفر مش معروف")

def getname(Id):    
    url = "https://shop2game.com/api/auth/player_id_login"
    headers = {
        "Accept": "application/json",
        "Accept-Encoding": "gzip, deflate, br",
        "Accept-Language": "en-US,en;q=0.9,en;q=0.8",
        "Content-Type": "application/json",
        "Origin": "https://shop2game.com",
        "Referer": "https://shop2game.com/app",
        "sec-ch-ua": '"Google Chrome";v="111", "Not(A:Brand";v="8", "Chromium";v="111"',
        "sec-ch-ua-mobile": "?0",
        "sec-ch-ua-platform": "Windows",
        "Sec-Fetch-Dest": "empty",
        "Sec-Fetch-Mode": "cors",
        "Sec-Fetch-Site": "same-origin",
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/111.0.0.0 Safari/537.36",
        "x-datadome-clientid": "10BIK2pOeN3Cw42~iX48rEAd2OmRt6MZDJQsEeK5uMirIKyTLO2bV5Ku6~7pJl_3QOmDkJoSzDcAdCAC8J5WRG_fpqrU7crOEq0~_5oqbgJIuVFWkbuUPD~lUpzSweEa",
    }
    payload = {
        "app_id": 100067,
        "login_id": f"{Id}",
        "app_server_id": 0,
    }
    response = requests.post(url, headers=headers, json=payload)
    try:
        if response.status_code == 200:
            return response.json()['nickname']
        else:
            return("ERROR")
    except:
        return("الإسـم مش معروف")


def get_status(Id):
    r= requests.get('https://ff.garena.com/api/antihack/check_banned?lang=en&uid={}'.format(Id)) 
    a = "0"
    try : 
        if  a in r.text :
            return("الحساب مش متبنـد")
        else: 
            return("الحساب متبند")
    except:
        return("الحالـة مش معروفـة")

def gen_msgv2_clan(replay  , packet):
    replay  = replay.encode('utf-8')
    replay = replay.hex()
    hedar = packet[0:8]
    packetLength = packet[8:10] #
    paketBody = packet[10:32]
    pyloadbodyLength = packet[32:34]#
    pyloadbody2= packet[34:64]
    if "googleusercontent" in str(bytes.fromhex(packet)):
        pyloadlength = packet[64:68]#
        pyloadtext  = re.findall(r'{}(.*?)28'.format(pyloadlength) , packet[50:])[0]
        pyloadTile = packet[int(int(len(pyloadtext))+68):]
    elif "https" in str(bytes.fromhex(packet)) and "googleusercontent" not in str(bytes.fromhex(packet)):
        pyloadlength = packet[64:68]#
        pyloadtext  = re.findall(r'{}(.*?)28'.format(pyloadlength) , packet[50:])[0]
        pyloadTile = packet[int(int(len(pyloadtext))+68):]
        print(bytes.fromhex(pyloadlength))
    else:
        pyloadlength = packet[64:66]#
        pyloadtext  = re.findall(r'{}(.*?)28'.format(pyloadlength) , packet[50:])[0]
        pyloadTile = packet[int(int(len(pyloadtext))+66):]
    NewTextLength = (hex((int(f'0x{pyloadlength}', 16) - int(len(pyloadtext)//2) ) + int(len(replay)//2))[2:])
    
    if len(NewTextLength) ==1:
        NewTextLength = "0"+str(NewTextLength)
    NewpaketLength = hex(((int(f'0x{packetLength}', 16) - int(len(pyloadtext)//2) ) - int(len(pyloadlength))) + int(len(replay)//2) + int(len(NewTextLength)))[2:]
    NewPyloadLength = hex(((int(f'0x{pyloadbodyLength}', 16) - int(len(pyloadtext)//2)) -int(len(pyloadlength)) )+ int(len(replay)//2) + int(len(NewTextLength)))[2:]
    finallyPacket = hedar + NewpaketLength +paketBody + NewPyloadLength +pyloadbody2+NewTextLength+ replay + pyloadTile
    return finallyPacket




def inret():
    global hidd,packet1
    print(packet1)
    try:
        print("success send")
        hidd.send(packet1)
    except:
        print("XXXX send")
        pass


def sendi():
    global snv,dataC
    while True:
        if '0515' in dataC.hex()[0:4] and len(dataC.hex()) >= 900:
            for i in range(400):
                snv.send(dataC)
                for k in range(1):
                    time.sleep(0.001)

            break

###

###
error = None
preventlag = False
sqlag = False
st = False
serversocket = None
clientsocket =None
inviteD=False
spampacket= b''
recordmode= False
sendpackt=False
spy = True
SOCKS_VERSION = 5
packet = b''
packet1 = b''
invite = None
invite = None
returntoroom = False
###





roomp = False
number = 0

def roompass():
    global roomp
    if roomp == True:
        return True
    else:
        return False

def roomst():
    if roompass() == True:
        try:
            return str(number)
        except:
            return "BYTE BOT"




#---------------------
from time import sleep

global cmode
cmode = False
def crmode(value7):
    global cmode
    cmode = value7
    return cmode


def crazymode(keam,pckt1,pckt):
    global cmodeloop
    while cmodeloop == True:
        keam.send(pckt)
        for fd in range(1):
            sleep(2)
            for i in range(1):
                 keam.send(pckt1)
#---------------------


def spam(server,packet):
        while True:
            time.sleep(0.13)
            server.send(packet)
            if statues == False:
                break

fivesq = False
def fivepe(value23):
    global fivesq
    fivesq = value23
    return fivesq


SOCKS_VERSION = 5


class Proxy:


    def __init__(self):
        self.username = "username"
        self.password = "username"
        self.packet = b''
        self.sendmode = 'client-0-'
        global connection
    def handle_client(self, connection):
        version, nmethods = connection.recv(2)
        methods = self.get_available_methods(nmethods, connection)
        if 2   in set(methods):
            if 2 in set(methods):
                connection.sendall(bytes([SOCKS_VERSION, 2]))
            else:
                connection.sendall(bytes([SOCKS_VERSION, 0]))

        if not self.verify_credentials(connection,methods):
            return
        version, cmd, _, address_type = connection.recv(4)

        if address_type == 1:
            address = socket.inet_ntoa(connection.recv(4))
        elif address_type == 3:
            domain_length = connection.recv(1)[0]
            address = connection.recv(domain_length)
            address = socket.gethostbyname(address)
            name= socket.gethostname()

        port = int.from_bytes(connection.recv(2), 'big', signed=False)
        port2 = port
        try:

                remote = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
                remote.connect((address, port))
                #print(" connect to {} \n \n \n ".format(address))
                bind_address = remote.getsockname()

                addr = int.from_bytes(socket.inet_aton(
                    bind_address[0]), 'big', signed=False)
                port = bind_address[1]

                reply = b''.join([
                    SOCKS_VERSION.to_bytes(1, 'big'),
                    int(0).to_bytes(1, 'big'),
                    int(0).to_bytes(1, 'big'),
                    int(1).to_bytes(1, 'big'),
                    addr.to_bytes(4, 'big'),
                    port.to_bytes(2, 'big')

            ])
        except Exception as e:

            reply = self.generate_failed_reply(address_type, 5)


        connection.sendall(reply)


        self.botdev(connection, remote,port2)

    def generate_failed_reply(self, address_type, error_number):
        return b''.join([
            SOCKS_VERSION.to_bytes(1, 'big'),
            error_number.to_bytes(1, 'big'),
            int(0).to_bytes(1, 'big'),
            address_type.to_bytes(1, 'big'),
            int(0).to_bytes(4, 'big'),
            int(0).to_bytes(4, 'big')
        ])

    def verify_credentials(self, connection,methods):

        if 2 in methods:

            version = ord(connection.recv(1))
            username_len = ord(connection.recv(1))
            username = connection.recv(username_len).decode('utf-8')
            password_len = ord(connection.recv(1))
            password = connection.recv(password_len).decode('utf-8')
         #   print(username,password)
            if username == self.username and password == self.password:
                response = bytes([version, 0])
                connection.sendall(response)
                return True
            response = bytes([version, 0])
            connection.sendall(response)

            return True

        else:
            version =1
            response = bytes([version, 0])
            connection.sendall(response)
            return True




    def get_available_methods(self, nmethods, connection):
        methods = []
        for i in range(nmethods):
            methods.append(ord(connection.recv(1)))
        return methods

    def runs(self, host, port):
        var =  0
        s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
        s.bind((host, port))
        s.listen()

        while True:
            var =var+1
            conn, addr = s.accept()
            running = False
            t = threading.Thread(target=self.handle_client, args=(conn,))
            t.start()

    def botdev(self, client, remote, port):

        idinfo = True
        p1 = b"\x12\x15\x00\x00\x00\xd0F\xc2\xd4A\xc3\xd9d\x98\x01U\x0b\xca\x9a\xc3\xfd\x96\x8c(\x8e\xb9tl\xd4\xda\xa4\x9c~T\x0f\xa9\x07\x11I\xbf\xc6/k\xf5\xcd\xa2\xea\x8c\xb6\xbe\xbc\x83&\xcaw\xa8\x83\x0cZ\xd6\xc7p\x8fAR&\xd9\x95\r\xe33B\x0b\xc8\xa7\x90i8\xf3\xb4\xb4\xb9\x1c\xfa\x19\xd1S\x8e\xdd\xd5\xed\x0f\xd4\xe1\x14H\xbb\xca\x00\xea\xca\xb0\xb0\xa4\xd9@\x8cj\x1a\x97\xc8\\\x05\xa6\xe0A\x82\xe3\xb7>)\x06d\xd2]\xe8\x1fvz\xe0\xb1\x16\xefVU\x98\x98x\xd2\x8a\xe7\x0c%H\x1a\tfr\x03b\x83\xc4Gn\x99\xf3\x19 <p#Xt\xc9\xfe\xd4\x83\xe1\x87m\xfe\xb5\xd4\x05U-\x91\xc8\xc0f962\\\x02\xe1\x15\x9f\xfc\x87\x9d\xb6\x05!\xa7Q\xb2\xef\xce\xb3\xa7\xc74\xaf'\xa6\xd3\xa0\x7f2\xdfg\n!"
        p2 = b'\x12\x15\x00\x00\x00\xd0mt\xbb\x1b\x04\x8e\xfeI\xd8\x16\x8d;4\xb4\xe0+\xf6]\xa78\x03\xf1Pf?\xac\x8c\xbb#\x95\xf4\xc6\xbb\xf2\x90\x1dO\x824\xeam\x99\xaa\xc7\x8d\xc9\x02\x8b\x81\xa7T4\x85o\xe9\xe4pTf)7|\xa7\xda\xd3\xb6\xa8\xe4\xefsb6\xd4\x01\xe2\xd4\xfa\xd5\x04\xa68\x95\x0e\x81-\x80^{\x81\xd7\x1e\xd0\xa3\xa2\xe1W\xeeE\x1009\xb9\xb2\xd0@a\xc6[\xba(\x7f\x07?V\xac\xe7bv\xd5\x83\x88\xee@L\xf6\xa7z\n\xe3\xca\x17\xfb\xa6\xd2\xa5$|\xed\x8e\xa2\xfc\x9d\xf5\xbd\xeaa>\xf5\x89\xc1\x08\xf2\x9a\xf8M=\t\xe6\xe3\x0c\xba\xfc\t\x8f\x1c\xf6\x8b\xa4\xe1\xc0\xaea\xa9\xff\xbf\x8ahe\x15\x96?\xd9\xea\xec0\x15\x9b\x03b\xb9\xb9\x84\x1eb-#\xa6]\x9b\x98,\x89\xde\xf0p\xdf\xe0l'
        p3 = b'\x12\x15\x00\x00\x00\xd0\x04\xb9\xf5\xd9\x08|\xa4%2N\x95\x87\xe5,\x0c\xd3o\xa2\xc5\xd5\xe1\x15W$\x9c\x8d\xb1\xef+)\xc4\xaeh\x9cx[\x18\x19\xe4\xd9\xdc\x82\xd1U\x1dtm\xef\x0fh\x91\x08\xcd\x108\xcf\x01\x97\xcf\x1f\xe8\x05e\x7f_\x03"\xca%\xcf\xc4\xa8%\xdd\xf8\xacj\xd5r\xf9p{\x11\xbf\x02Q\r\xca~\xd8\x0b\xaf!\xfa\xd0\xa5T\x98\xda\x94\xc2\xcf\x1a\x95\xd7\x12\xef\x9de\xed\xaf\xf29\x1e\xfd\x1f}p\x1bI\x8f\x1bt\xcc\xf2m"X\x9b\x8fj\xbf#M!\x80\x8e\xe32a\xcc\xb8\x1c\xfe\x0c?p\x91\x8dM\x83\xa7\xe8-\xcf}\'\xa7P\x05\xa5\xe6\xe1O2n5]\xbbZ\x80\xc5.h\xa3v\xf3\xae\xbd\xc2\x0e\x10\xc2v\x92\xef\x9c\x191\x1c\x90+\x0c\xb4&L\xdc#Q>M_\xe80\x98\xa9\xde]'
        p4 = b'\x12\x15\x00\x00\x00\xd0?\x1a\x92\xa0\x7fa\x83-\x12^xW*\xf8(\x9aBY\x13\xa0&\x90av\xa3;K8\x91\t\xbfj\xf6\xd8Z\xdfk;\x9c\xfe\xb5y\xec.NZ\x06A\xeag\x94b\x98\xd9EpP\x8b4:i\x14\x80\xb1\x1a\x8c\xda\xe9\xdd\\\xf6;\x11\xcc`Z\xe6\xbc\x8ef-\xfc\x9a\xbb\xe0\xfa\xfb\xa3\xb9\x0b\x9f<V\xbbq\x08u\x9d\x93\xc4\x12|\x96 \xf9k\xc2\x19\xc2\x80-\xc2\xf1TI\xec+\xc9\xecD\x0e\xcb\x15\x02+\xef\xe0\xc9"\xab+6\xd4\xcc\x86\xb6ee\xa3\xd5\r\xc3Z\x1a7\x94\xc8\xb8V\xcbS7\x9c?6K\xce\x9c\x03/\xceRY\xf3\xf5\x8b\xe3\'uVsw{`um\xc4\xd9sIc\xfehW\xc0d\xc9\xfa\xcfk\xbd\x8a\xc2\xdf\x80\xbd\x86\xc3s\x0c\xfc\xa9\xd3+w\x89\xebv'
        p5 = b'\x12\x15\x00\x00\x00\xd0\x04\xb9\xf5\xd9\x08|\xa4%2N\x95\x87\xe5,\x0c\xd3o\xa2\xc5\xd5\xe1\x15W$\x9c\x8d\xb1\xef+)\xc4\xaeh\x9cx[\x18\x19\xe4\xd9\xdc\x82\xd1U\x1dtm\xefC\xd7\xf6A%r$\xb6\x05k\xaa\xd7\xcf\x8d\xfd\xe6V"FN\xe7\xeek-\xb2\xef\xad\x90\xde\x04\x87\xc1[\xba-\t,\xa3yY)\xb0U\x97=\xc1|\xf5\x16*\x9a\n\xc5V\xd0\xb8/\x9dVd~W\xda\x1e\x98d^)\x1c\x01&\x8c}87b5l\xb5\xe4\xd0"\x92\xac_R`\xe7\x9fh\xb7\x1ed\xa4P\xd7\xc9J\xbf\xb7&[F)\xd5\xba\xdcU\xfb\xa6\xf9\x82.\xbb\x00\x0c"\xe6]\x88\xcce\xd7\xc9\xe7\xc1Y\xbc\x07\x11N\x9fu%\xa6B{\x19\xf3\xc4\xd3\x046m\xbbt\xcf4o\xc1\xd3x\xc3\xa3/\x97\xe8`5\x0e'
        xmoodz = b'\x12\x15\x00\x00\x00\xd0F\xc2\xd4A\xc3\xd9d\x98\x01U\x0b\xca\x9a\xc3\xfd\x96\x0es\x88\xa5\xcd\xc6V\xaf\xf5w\xf7\x85d.w\xc0JN\xff\xa1p.\xed\xd9\xd9iw\xc2\x1c\xa3\x96tO\x8f\x02\x02\xea\x03\xbe\x08y\xe6 R\x84m\xc9\x0e\x81\xe0\xc4\xcc\x82\xe0\xa3P\xeb-.\xf5\x8c9Q\xb6V\xbaL\x03\xa44\xbb\xbc\xe7\x01\xb4\x1b\xd47b?\xd9\xc2Y\xde\x1f\xd4\\\xfbY\xa5,\xbc\x1f\x15\xcc\xb9\xcc\x11Z\xc1\xdc\x96\x03\xf5\xa0\x10\xa5\xec\x81\xc2I;\x82\xa7\x87\x0fI\x93Z\xec\xda(g\x88\xd0\r\xc4\xc08\xd5\x01^\xdfy+W\xc8\xdcb(\xba\xdf(\xd1A\xb0\xe5H\x08V\x1eQ\xe8\xe8Bw\x01\xae\xec\xc7\xb7\xd0\xb8\x13?VG\x83Uh\xf4L\xdc\xe0\xf7Y5\x89\xad\xf6\xf9\xd7\xed\xbb<\x98h\xaca\xa3<\x04'
        p6 = b"\x12\x15\x00\x00\x00\xe0\xd8\xe5Q\xf8\xd6\x92J\xeb\xdf\xd9a%\xa6\x95n\x006\x81R\x85\xdd\xb24\xb3\x19F\xae`\xdcJ\xb5\xe7\xee\xa9\xa6\xe1\xb53\xa8~\xb8\xaa1\xe8\xe4\xfc\x9c\xb6\x94[\xec\xca\xaa\x1867%=5\xc2&\xb5\xe9\x88\x1cU\x0frBg\xa7\n\xc6\xfa)5\x8a'\xce\xa0\xd3\xbc\x1a0\xfeOS\xca*@\xb8\xbe\x91?I\xe3\xd0\xc0]\xa3\x13s\xdc\x1eG`@\xe2\x91yy\xb7\x85\xb9\xd6\xdd6\xa1\xfe\x9c\xf2\x8e\x83\xb1R\xd8e\x9b\x8e\xa4\xa9^\x10N\xd6\x9c\x91Y\x0e\xe4\xf1\xab^\xe4g\xf4\xbb3\x86\xa7\xc6\xed\xe8\x10\xc4\xc4\x03X2;N~\xd1uDa\xe4\x94_=\xd5E\x91\xdc\xfb;\xc7YFFQ\x85\xaa\xbcB*\x16\xb0\x08\xd9\xb4\xca0\xbb\xde\xce2\r-\xee\xa1i\xe5\xce\xa7r\n*4\xbb9\xa4=u\t\xd8\xf5\x88\xd9\x14\x80\xec\x04\x07"
        p7 = b'\x12\x15\x00\x00\x00\xd0\xb7\x0e\x99\xe1\xac\x10\xb1Z#H\xae\xc1\x92\x7f\x80\xf6y\x92\x98\x1e*\x1e\x15\x17\x98V\xa2\xd81\xaf\x86\xce\xec\xefH\xae\x0c>\x0f\xfa\x9fVl\x0e+"\xd7\x94-9K\xb5cJ\xbf\x9c\x12\xe2\xfe=\x8f\xcd\x1c53\xda@/\xf4R\xdb\xcc#\x90{[\xb3\xa9\xd97\'\xe6%\xb5\xb8t\x17\x07\xd4R\xe8\xaa\xeeP}C\xf6,\xc3\x1a\xa6cl\x88\xe7\x99\x9b\xb2\xf3\xbf\x19\x8b,\xc9\x97T\xfaD\x08\x89\xb6\xe5 ^\x95\x9c\x90\x1f\x04\x84\x0f1\xea\x9fdnA\x04\xf1\xba\x9bc\n9Z\xcfy\xf8\xbeb\xd7\xcb\x16\x0e&#\xb6\x1e\x1d\xf0 K\xde\x15\x1a*QD\xe2\xfd\x0e\xaf\x08\xb4(\x89}\x14q\x94\xd1\x9b\x99\xedi\x00\x8e\xfaT\xa6J\x91\xcf\x84\xa8p\x88\x89\xa5\xd1\x7f\xf2\x15\xcd\xe7\xece\x8b'
        p8 = b'\x12\x15\x00\x00\x00\xc0p\xdd\x00\xbd\xde\xc4\x96p\'\x13Vb\xce\xe2\xf4\x10\x15\xff\xf2i\xb2\xe2\xfd\xa7U\xf4\xe9I\xdc\x04wM\x90\xce\xe3X\x98\x96\xcf\xd4\xa2tS,\x1f\xfc\x8b#\xc1h\xc6>\x86\x11G\x87\xe5\x9c\xd3\x90\x92oT\xe1\x90\x8d\xd3\x1d\x07\xf8\xcc/\xcf\xfc\r\xcf<-\xd8\xa7\xc2]\xa1m=\xb9H\xc0\x89\xef\x9d\xc8&\x0c\x84\x9f^"\x8d\xd7u\x99dx$\xf9\x8a=pl\xc8\x9f\x8f\xd2T\xc6\x84\x05\x94\xa3\xbdo\xffI\x8c\'\xc9\x88\xb7~\x04{\x1a\xae\xe0\xdc\xe6\xbb`\xa7\t\xcd\x11H\xc2O\x8f\xa8\xea\x8c\xb5\xb9\x1a\xf5o\x95\'\xacf\x16\xed\x02\xa5\xcd\xb1\xc1\xc9\xec\x1b&gsSV\x9b68\xb3\x97\'b\xc5\x7f\xf5\xfcx2\x0c6\xce\xc9F'
        p9 = b'\x12\x15\x00\x00\x00\xd05X2\x11\xb5\xe9<\xbdM\xd6\x98p/R2\x03\x06V\xf3\xd6\x17O\xf3\xef\xfe\x8e$\xf4\xcd[.0\n6\xc5\xb7\x12\x9a"\x8b\x04\x93\xa0\x9e\xce\xc7\xcc\xc6\xab\xe2\xa9\xb9\x03\x9d\x86\xb0\x0c\x89\x80\x82a\xd5\x83\xce\xaai%\x17\x12[\x95\xdci\x1b\xa3~\n\xe9\xf7s\'\x04\xb0\x0c\x8c\xc9\xdf\xb1\xb1%\xbe\xe2\xa1\xa0\x0fN\xe5 \x92\x1c\xbb\xa47\xfd\x13\xfa\xc3>\xe9C+\xdf%\xf4x\x14\xdd8\xe6\x91{m.S=\xd2\x7f\xc1(\xfaZ\xdf\xf7\x9a\xc1N\x9b\x13\x05\xfa\x08J"\x1b\x98\x19v\x0c%\xa1\xb12\t\xfe\xcf\xa4Ta^\xd7\xa3\x9b9\x8d\x8cN>\xf1\xde9\x94!\xdd?\x19\xfb`\xbb\xd1\x9fc\xfev\xe9\x10\x073\x9c\xda\xd7@0\x05\xfdg\x87\x12.\x95*\xa6\xe5\xd7\x81P\x0b\xd5c'
        p10 = b"\x12\x15\x00\x00\x00\xd0mt\xbb\x1b\x04\x8e\xfeI\xd8\x16\x8d;4\xb4\xe0+k\xe8?\xc0\xe9.\xea#u:\x87\x83q)?%\x87\xc5\xc49Q\xa2\xe1V\x17!7\x85P`\x93\xa3\xf9\xb7\xea\x8b\xd0G\x82\xe7'\xff\xdbZ\xe7\x16\xde\x8c\xab\x03F\xcd\xf6V\xb0\x0e\xdc\xfdT\x84\xfc\nf+\xf5u\x8f\\\xba\x049\x7fi\x06\x9c\t\xbdH\xe3\xfd\xdc\x9f\x15j\xf3`\x02\xfd\xb7:M\xda\x14\x18\xf2U,A\xef\x0e.\xbc\xb4\x12\x961\x9d\x1a>\x8c\xc8\x00t\xd9\xbe\x07c\x0c\xa31\xd5\x81W\x98\r\x1f1p\x96O\xd5\xd4\xe5\x1b\xbc\x19\xa9\x8d\xcf\x9c75\x14\x16x\xca\x8c\xf9\xe6&?\x00\xd0U0}\xb7\x8aq`\x1f\xd7ll\x15\x10Y\xa00\xfa\xd0\xf6e\xe3\xa9jz\xc9^v\x90nO,\xb2\xc6M(\xfe\x07\xa8q"
        p11 = b"\x12\x15\x00\x00\x00\xd0mt\xbb\x1b\x04\x8e\xfeI\xd8\x16\x8d;4\xb4\xe0+k\xe8?\xc0\xe9.\xea#u:\x87\x83q)?%\xe9\x1e\x92|*\xfe\t6\xca\x0c\x9f\x98\xb9\xf1$}\xb1K\x80\x1cT\xe3+\xc3u\n\xb0\x9c\xd0\xaa3hDE\xfaWd9Q\rz{\xc9\x90\xe4(e\xf2\xcdI{?2Y\x18q<\x05\x80\xde3\xfc\x02\r\xa4fCVQ%B\xb2\xe3\xde\x82\x1a\xa1\xf1\xa7\xa2}4\xbb\xa4\x15\x93v\x9fL\xc5\xa2\x9c\x82a\xf5\x91\xba\xcd\x89\xbc\x94\x92=\x88\xca\x03%#|\x06\xe6\xf0\xb3Ad]J\x81\r.\x84f\xde\x96\x14\xab\x82E \x1b8M\x1d\xeb\xda\x17\xb9Z\xd9\xe8\x05\xc7\xe2o\xbc\x8bz\xa1\xa7\x00L \xc1\xb9\xc9\xc8\x8e\x01'\x07\xf31\xfb\xc6+^0\xcc\xd9\xc8\xcb\xcf\xcaCt\xb1"
        p12 = b'\x12\x15\x00\x00\x00\xd0mt\xbb\x1b\x04\x8e\xfeI\xd8\x16\x8d;4\xb4\xe0+k\xe8?\xc0\xe9.\xea#u:\x87\x83q)?%\x8bAJ\x1cZ9\x8a\x15L\xd4Wcv\xfe3\xc25<\n\xba\xedf\x96\x8b\xfc\x9ei\xc9y\x8a\xab\xa4\xdf\x05F\xe2I[\xb5#*:t\xc5\x89\x91R1\x14c\x83R\x8b\x10V\xceBSA\xa9D\xad\x9eA\xb0\x8e(\x82J\xf1\xdf\xd0.\xb6@\xfe8&\xdf\xa7\x8c>\x02\xc4\x13\t\x82x\xb9}\xf9:\x9d\xa7P\xbf\xd5\x04\x1d\xa2\xa8:\x0e2J\x01^\x14S\x89\xdan\xd4\x8cb\xa3\xdd\xb7\xba\xc2\xa6\x99{\x7f\xff\xc4\xdb\x00^\x80M\x08\x1d\xf8\xa8\xce\xb9Oi\x15Sg\xc4\xa3\x12xHN\x84N`\x01F\x91\xb8\x16\xbdVc\xf6\x17\xd1\x92w\xed\xa3\xdb\x1c\xb0\xe0h\x17\x7f\xd0J\xfe'
        p13 = b'\x12\x15\x00\x00\x00\xe0%XH]\xfc\x99V~^(yl\x93\xf4L\xa8\x10:z\x11\xd9\x8a\xca$]\xa5D\x84\x84\x83C\xb9\x07\xb5(to\xce\xc7\xf5\xf8\xdc\x15\xad;\xec\x15\x88h\xf6\x88I\xb7\xfbC-AaWI\xff"\xcdA\xd4\xd1\xe7<\xe3n~\x13\xdds\xc2\xc9s\xd4\xef\x91\xe0\x84*D^\xdf\xd5\xe8A\xecN\x8bu&%7\x90\x9f\x8d\xe6\xe7\x17\x93U\x9ad<^r\xd6E0-Ay\xf15H\x1d\x17\xc6|\x12\xac\x8c\xd8\xc4^I\xb5\xdf\x8dy\x0b\xae\xa4\xaf\xbb\xec}%\xc4\xb3\xd2\xb0$\x92\x9f\xe7Z\x16\x81C\x9a"\x8e/\x18\x9b2\xe5\xb9\x80\xba\xf3\xd65uI\x91\x15\xa4\x98\x87@\xa7\xb1!\xff\x9f\xfc.\xca\xb0\xbfj\xfd8R)b\x8b\xe2\xd0\x08\xc3\x83+\x13\x03^\x11\xaa\xd1\xd2w\xd3\x18T\x9c\xeb[vf\t1\xd54\xc8\xcb\x1d\xb1u\xdd'
        p14 = b'\x12\x15\x00\x00\x00\xf0\xee\x02\x9e(G\xc5\x0f\x8f\xdb\xeb\xeaj\xdb?\xf0\xd2\xadc\xac7\xfc$\x8a\xaa\xd9WK\xe793\xe0\x9f^53\xe6\xd0?\xaf\t\xfdS\x1f*\x03\xf1\xfb\xb6\x93\xb7\xb0\xaef\xb5\x14\x86\x0e\xf5\x96}\x17\xde\x8a\x19\xac\xee}\x00\xbaF\x18!\x95\xa5\x1c|%\xc7\xc8\xca4\x059\x82\xfe[\x8cU\xda]\xf0]\xd0\xf8\xe7\x06\x08\x08\x84:\x95\x111\x0f+*\xd2\xdc@~"\xc3yG:\xed_\xa1\x1f\x07d8@\x04\x9c\xc9\x87\x96\x16\xd0\x99\xa5|3\xb3\x8a\xed\xf9\'\xf69h\xcd\x8b\xba<7C\xb4~\xf8\x00\x04\x9ct1\x1a\xc8Ken\x9e\xc5jn\xec\x8c\xa5\xb1rA\x87w\x87a|p\xe5\x05\xdc\x16\xd7\x99n\xd0\x9a?\xd3\x17p\x06u\xfd\xce\nO\xd7\x9b\xe3v\x15\xa7[b\x84\xc3p\xfdT\xa5\xd7=\x11DW\xbf\x0c\xbe\x87\xa9\x16\xeb9\x9e\x1a\t\xda\x17\xf8,\xc5\xc1=&\x94\xe1\x0f\x0c[\x1e'
        p15 = b'\x12\x15\x00\x00\x00\xe0\xd5\xf8\x86af\xfb\x13\xb5\xf2\x9bT_\xf8\xcb\xab\n\xe4\x93\xd0\xbcF\xb0\xad\rL\xbb+"\xf6\xe45skH"\x1b\xb4\x8edT\xb5\x9f)le\x8d\x8cw\xa9q\x9e\xed\xf0jd2 s\'\xbc0g\xbd\x9d\xceQ,ACo;r\xe3\x1d\xa3C\xa3\xc5\xd7\xdf\xb9P+\xfe\xc8}\xef_\x85\x163\xb4@]|\xc2\xfd\x89XX/V\xb5\xf6\x85\xd6j\xb0\x96\xf9\xd9\xab\xd9\x8e(\x87]\xd6\xa1$0\x97WE/$\x97\xe7\xa0\xbeI\xf65\x0cV\x1a\x81\xe5u\xaa\xd93\x97\xde\x00\xeb\xb4\xef\xfe\xabf<\xdb\xcfP\x9c\x9d%1\xa42k*v\xdb^C\xc0 \xa4\xd8\xcab\x97cD I\xf3\xb9\xf0S\x18\x06\x8f\xbe\xb1\x0eA\x0c\x0c0\xfd,\x06&\xf7\xf3\x81\xf7\xce\x9a^oni$\x05\x9a\'\xb5\xc106\x81\x90\xb3`_H\xe6\x91b+'
        p16 = b'\x12\x15\x00\x00\x00\xe0\xae\xad0J\xdd\x0bLR~\xe2\x16\xa9%dOu\x1e\xf9\xd9R`\x01\x88\t\xb3\xb1x\xfd9\x8a\x13\xf2\x86Q\x91\xe3\x89z\xffk\x08\r.R`\xc5\xb51\xdc\x1a\xa1[O\x11\xda N\x1at$\x9f\x1c\x00\xa1\xcf\xae\x0e\xcf\x0e\xcfOX\x06\xf1\xc7c\r\x95\x03G<\x9cj\xa5\x18\xf5!\x16>\xee\xb9\xa1\xcd\xa9\xcc\xbc\xa8li\xb7\x0f\x05\xc6\xd2Ns?\x9d\x10\x12c\xaa$\x17\xe8^\x17\xab\xf9De\\\xa8\x82p\xa3\x14\x81\xb5h\xb0\xef\xe3\x04\x9e\xce?\xa9\x0fCE\x03~|s\xf1\x84\x82dM-^O6{*\xde\x14\xe2\x8d\xcei\x0bWV(\x01\t-\xd6\xbe\xa1q\x1ay\xcek\nvc\x96\xf5W42\x91\xc2\xa7\xce@ \x1d\xf3\x80\xe9\xc47\xa3F\xf2\x95eZ\\\xaf<\xc9O\xbb\x1e\x14\xe4\xf1\xff_\xf8\xb0\xaaz}Xw\xc4\xab'
        p17 = b'\x12\x15\x00\x00\x00\xf0\x92\x95D\xf8\x9b\xa2-PD\n;\x05`\xe5\x1a\xefFS\xd4\xe1\x97_.5\x93Q\x96\xb7 \xb0\xa5D\x16\xbck\xe7/P(\xbc\x02\t(\xdc\xb8\xa0\\\xfd\n-\x89D\x14U\x00\xeb\xb7\xeb\xffcu\x9b%(\x92&\xb4\xd3\x86n?\xdc\x91\x87\xef\xf1\x81\x94\xf5b\xffTKh\xf1&\xce\xe0\xfe\x19\xc6\x9b\xcf=Y!\x02o\x93!\xbf\x94\xb9\x8at\xf5\xc9\xddp\x8d\x9f&\xefOs\xe0\xf6\x9c\x9eg\x85\xd6C\x00\x96Oi\xe2\xf5\xf5\xe1l\xf7\xcd\x0b\x8c\xe5x8\xb1\xb0\xdc\xfe\xeb>\x94Z\x11\x0e+#\x01\xe8\xe7\xa5\x16\x18c2$\xfd\xc65w\xc6.\x88\xcd\xcd\x04\xd5\xe9\xce\xcf\x1d\xd3\xa9\x1f\xbf\xa0\xd2\xcf\xe2\x0c\x19\xf7\xc7\xd8\xed\x83\x16\xfd\xc1r\x8d\xf8\x97X\xcbz4\t}Qg\x197\xe7D\x86d\xd0C\xedU\xa4P2b\xf98u\x19=\xd7q\n\xe3\x93\xb5\x8f\xb46\xb7\xad\x9a\xb81\xf7w'
        p18 = b'\x12\x15\x00\x00\x01 K\t\xd9\xa2\xd2\xbajc\r7R\xb1\x0c\xba\xd9K\xb0\xcf\xd8\x05\xff\x80\x82g\x05\xdd\xcb\xe7\xd7\x97\x13?d\xb1\xc4z]=!\xbc\x11\xfe\xed\xd7O\xa7j\xb1L\x1a\xa6\xbe2\x8aa\r\xacX&\xcb0$W\xc7\x1d7\xc8\xcf\xf8\xb9P\xfc+\x16\x1fJ\x05\xe6\xe1\xe2E\t\xaf4K\xcb<\'#\xba\n\xec\xf9\x1ac/0\xcc\xb4)\x7f\x93\xc4\xc6\xba\x92\x02T`~\xed#\xc0\x19\xef\x0b\xbe\xc0;zo\xf6G\xd2\x88\x88\xebL\xaa\xbd\x9f\xae\xa2\x16\xbc[fm\xe5 \xa7\xbd_\x12\xdcd0yn9\xe4\x1a\x08\xbf#\x80%>X\x91\xdb\\\xd6\xc5-\xd3\xeeD\xaa\x9a\xc4\xfej&\x99\xe0\xed\xb3\xc8\x92\xcc\xed\x87G\x94R\xb1\xddMYUp\xdb\xb3\x96\x85\x16\x83\x05T\xf1\x80o&\xb7V\xa8X\xa5\xd1\xfag\xbd\xecvL\xc2\xdcG\x9f\x9br\x0f?\x01\xefc\xe1<\xd9\xa4\xd8]\x0f\xd2\x12\xc4\x15\xc7\xb1\xad6\xc1\x9e\x13.\n\x8f\xfa\x7f9\xea\x1b\xfa\xdb\xa3p\xc7\xda\xb0\xe3\xa9"+\xaa\xbdhzd\x1a\xa6\xf6\xee:\xb1{B\xe0\x19B]1\xd9\xe6)\x17\\\xe8'
        p19 = b'\x12\x15\x00\x00\x01 .\x02w"81\xf5\'\xf1\xd7\xf1\\4\xf7"|\x94\xde\xfb=\x07\x81\xac)\xf3\x18\xb4\x14\xa8~X7\xe2\x04\x1fH\x0b\x08M\t\xbc\x1d\x91\xc4?z8\x9dm\xa2\xdc\xbe\xf9\xb2v[\x87\xe1\x0e. \xf3\xb3[\x19N\x93cD,.\xf7\xe5\xd2t\x1f\xf5\xffH\x85I\x0fj\x99N\xbal\xb9\xd2\xf2\xffw#\x1fo\x98O\x9e\xf5\xc6\xe9#}\xa2\xea%l\xdec{\xe6yo\xca\x88\xc8\xd5 \x00\xb1;c\xe1\xa59\xcf\x97\x9a\xd8\x1f\xec\xe6\x85\xce\xc41{q\x842)\xf8\xc6\xb41\xfe\xed\xaa\x13\xccFs.xY\x89sf\\B\x16g\x0bp,\x06*\x12g\xf3C \xc9\xcc^r\xa7\x8b\x83W\x10v\xcf\x00\xf1(w+\xfd\xbc\xac#\x1d4\x9d\xdeb\xa9\x00!\x98\x8e5\x86\x1d\x00\x1e=\xcb:\x19\xf6f\xc6\xc3\x078O\xbd\xf4\x85yD3h\xaf\xd7\x97\x19T\xc2<\xdf\xca\xe3\xec\x95[=~ZxJ<\xdd\x0b\xe1#,w\xe8\x064M\x19\x13\x94-\xb7e\xa8\xd2\xbcW\xa0\xa6\xed\x82i\xf4\xd2\x02\x1b\xe431-8\xb8\xc7\x8b \xf7\xb3V.|\x11'
        p20 = b'\x12\x15\x00\x00\x01 \xbfG\xc8|\x90\x0c\x00*IB\x9a\x06\xebi^\xba\x81>\\x\x00\xcc\t\x85\x8bC\xad\x1a\xae\x1d]\xfd52\x87\x18\x88j\x0e.\xa2\xba\x18/\x95\xf2d\xf2\xef\xb5\x9f\xb7\xb4\xfd\xb8\xa8:\tF!\xef4*\xd2R^z\x91P\xb9i\xfe`d\x9f`l\xa8\xa6\xafq\x0c\x80\x00J\xbd\xf9\xc3\xf7\xee\x9e\xe4\xaa*l%\x94\xa8\xca\x15\x9d\x0f]\xd1-\x80H\xca\x11\xc2\xfd\xad\x07\xbc\xf7\x98\xff\xc9 \xe1\xf7\x12\xaaR\xc5\xdd\x11V\x05V\xbb\xb7U;.j\xf6%\xbe\x97\x1a@x?K\x1b\xef\x1d\xfa\x05\x93\xd0\xeel\xba\xbf\xf7\xc4\x1eqrl\x18n\x1a?\xac\x9br\x0bg\xe7\x97\x14\x85HV\xad\xd2\xb5\xf9\x1a\xbf\xaf\x1b\x9dYi\x166\xb9Ar\x9d\xf2\xbdt\xc0\x14\x10\xd7\xd2\xad\x05\t2\xb5\x111C]5N\xa7\xca\xb7"\xca\xb5@y\x8a\x97_J\x89j]zk\x82\x8d\xff\xe81f\xee\xf4\x86\x04&\xcer\xde6\x8b\x98\xb1|\x16\x9f\xb9W\xb7\xbb\xa8%\xd3\xa7J\rR\xcb\'\x10\xd1@[\xe9\xfb\xe1K\xfaDm\x88\x05\xe7\xd1\xe7\xc9\x7f\xc6c\xb9\x9aD\x9c'
        p21 = b'\x12\x15\x00\x00\x00\xf0\x8d\xa3\xa1\x0c\x8c\xd9\xb9\xaa\xe6\x8bf\xf2\xe8S#\xfc\n-x\xf5H\xb8\x81\x15z\xf9\xf7J\xfc\xaf\xfb-\x15,\x0b\x06\x0eF\x89t\xec\xd4\r\xa5I\xba\x97\x91I`\t\x13S\x89)\xd07,=\x00\xa0|I\x18\x12\xa0\xf4\x95\x8e\xde\x95\xaa\xb9\xb3\xc1\x9b\xa6_\x8amF O-\xb3\xfb\xc3BC\xd1`H\xd0\xe8.\xb3!+&^\x93^Wm\xb5\x95\x07P\x90\xb7t\xb9\x8c\x8b\xb8\x98\xa3C \x8f6\xf5-\xb3\xd7\xef\x0c\xdb\x92\x01E=\xf6*\x96\xd6\nYg\xdb\xcdm\xac\xda6\xc2\xc0\x83\xe4\x80l\x15\x8f\xfe\x1eG\x9b\x03Xi\xf2\xc9|\xd1\x17\xb3K\x13u\x1c)~\xa5\x19\xae\xa0w\xc3\xfdW;_H\xda\xce\xbd\xb3\x93$\x8d\xf6\xf2Ir\x1b>\xfa`|C\x1d)\xf8\x8dKRP\x1cu\x99\xad?1\x0f\xb7\xe7p\x13\x83,\x1d\xca\xdf-\xc1\xb2\xf4\xc8e\xe6\x84\x0b\x0cQ\xfe\xecp-K\xf2'
        p22 = b"\x12\x15\x00\x00\x00\xf0+\x8e\x91\x82\x12\x94\x1fP\xb7N\xb0K\x88\xb6\xdfU\x0b\\\xd6a\xb0\xd5\xf1\x81/\x13\xed\x8c\xa7<\x83[=rV\xd6\xad\x13\xb3\xdeC\xd6\xdfP\xe0\xe47\xb39\xd9:v\x16\xd0\\2\x1a\xea\xf5p\x14J\xc2\\\xc5h? \xfc\n\xa9^\xeb\x19Z\x85\x99\xaa\xb3JE\xde\x81\x93\x15\x9b\t\xcfQ\x8f\xaf\x1e`\xd32\x19\x0b\xd3\xb3\xb7Bk\xb7\xd5\xb9\x03\xect*s\xc4I\x84\x0f\x8cX\x11\x7fY\xc0\xef\xd3*\tEE&\x07\xbfs\x1e\x0bp\xc1\xc0m]\xe4\xa1\xe3\x91\xe4c>|\xbd,!\xd9'\xb5\xfdy\xfb\xcdmK\x0c\x1f\x14\x874\xe20i\xebN+t\x06Ef\xd8\xa3]\xec\xa3\xb6B\x1aq\x1dW\xf3\xc5xei[\xb2\x1aS\xbe\x9f\xe6\x98x\xc7\xdf\xeb\xcb'\xdd\x19\x0eeWu\xb3\x9e\x1e\xe7\xdf\x8bw\xf7D\x04\xa5_\x1e\xc9dmw#\x1c\xe5n\xe15S\xfc\x11\xf7@l\x92z\xee"
        p23 = b"\x12\x15\x00\x00\x01\x00\x00\xcc\xee\xca\xa9\x07B\x91\x86\xdb\xaft\x0bAH{0E\x01\r\xda\xf7S\xb8\xf4\x80~\xb2/\x99o\xaeX3\xfe`\xf9&\t\xd3Z\xaa\x1a\x814\xd8f\x8c\xda?t\x04\x17\x17cAE5~\x03q\x86>\xf3\xc2*\x1fq\xa2\x04\xf2.\xe6\xeb\xd70\xa1\xe62W\xba\x86\xde\n\xe18\x86>\xce\xb2\xebS\xc8d\xe9\x97\x18v\xc1_\xce\xd6\x98V\xc4\xaf\xc3K:\xd0\x80\xec3d\xb0>\xc5\xc6\x98L\x19\xe0\xa0,\x06x2{\x8f,\x19<\x9b\x1a\xb0|<\tgY\xb6\xa2J\x86e#<e\xdd\xc2\x97\xcfD\xbd\x83\x8aZv\x14\xed!\xc3\x1apV\xc5\x8f*E\x08\xae#\t6)\x0e\xee\xda\xda\x85\xa4\xf4N\xea\xc3c8\xf0\x186\xb9E\x18d\xe5\xcaY\xae\x9c\xef\xd4.=U\xa4rz\xf1\xdf\x8d\x80\x81\xd9z=\xf1v\xcdT\xe0\xa5Z\x91od>Y\x91\x1a\x91!X.=\x85\x19R\x85\xdc\xfb\xa2\xf3\xff\x8c\xaa\xef\xca'\xfd\x14_\xc6\xe1[\xf6\xc2"


        yout1 = b"\x06\x00\x00\x00{\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*o\x08\x81\x80\x83\xb6\x01\x1a)[f50057]\xd8\xb5\xd8\xa7\xd8\xa6\xd8\xaf\xe3\x85\xa4\xd8\xa7\xd9\x84\xd8\xa8\xd9\x87\xd8\xa7\xd8\xa6\xd9\x85[f50057]2\x02ME@N\xb0\x01\x13\xb8\x01\xdc)\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\tAO'-'TEAM\xf0\x01\x01\xf8\x01\xdc\x03\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x11\xd8\x02F"
        yout2 = b'\x06\x00\x00\x00|\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*p\x08\xd6\xd1\xb9(\x1a![f50057]\xef\xbc\xa8\xef\xbc\xac\xe3\x85\xa4Hassone.[f50057]2\x02ME@G\xb0\x01\x13\xb8\x01\xcf\x1e\xd8\x01\xcc\xd6\xd0\xad\x03\xe0\x01\xed\xdc\x8d\xae\x03\xea\x01\x1d\xef\xbc\xb4\xef\xbc\xa8\xef\xbc\xa5\xe3\x85\xa4\xef\xbc\xa8\xef\xbc\xa5\xef\xbc\xac\xef\xbc\xac\xe0\xbf\x90\xc2\xb9\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x01'
        yout3 = b'\x06\x00\x00\x00x\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*l\x08\xe9\xa7\xe9\x1b\x1a [f50057]DS\xe3\x85\xa4WAJIHANO\xe3\x85\xa4[f50057]2\x02ME@Q\xb0\x01\x14\xb8\x01\xca2\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x10.DICTATORS\xe3\x85\xa4\xe2\x88\x9a\xf0\x01\x01\xf8\x01\xc4\x02\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x0c\xd8\x02+'
        yout4 = b'\x06\x00\x00\x00z\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*n\x08\xed\xd4\xa7\xa2\x02\x1a\x1f[f50057]M8N\xe3\x85\xa4y\xe3\x85\xa4Fouad[f50057]2\x02ME@O\xb0\x01\x13\xb8\x01\xa9#\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xdb\xdb\x8d\xae\x03\xea\x01\x0cGREAT\xe2\x80\xbfWALL\xf0\x01\x01\xf8\x01b\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\r\xd8\x023\xe0\x02\xc1\xb7\xf8\xb1\x03'
        yout5 = b"\x06\x00\x00\x00\x84\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*x\x08\xb6\xc0\xf1\xcc\x01\x1a'[f50057]\xd9\x85\xd9\x84\xd9\x83\xd8\xa9*\xd9\x84\xd9\x85\xd8\xb9\xd9\x88\xd9\x82\xd9\x8a\xd9\x86[f50057]2\x02ME@G\xb0\x01\x05\xb8\x01\x82\x0b\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x15\xe9\xbf\x84\xef\xbc\xac\xef\xbc\xaf\xef\xbc\xb2\xef\xbc\xa4\xef\xbc\xb3\xe9\xbf\x84\xf0\x01\x01\xf8\x01>\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x05\xd8\x02\x0e"
        yout6 = b'\x06\x00\x00\x00\x8e\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*\x81\x01\x08\xeb\x98\x88\x8e\x01\x1a"[f50057]OP\xe3\x85\xa4BNL\xe3\x85\xa4\xe2\x9a\xa1\xe3\x85\xa4*[f50057]2\x02ME@R\xb0\x01\x10\xb8\x01\xce\x16\xd8\x01\x84\xf0\xd2\xad\x03\xe0\x01\xa8\xdb\x8d\xae\x03\xea\x01\x1f\xe1\xb4\x8f\xe1\xb4\xa0\xe1\xb4\x87\xca\x80\xe3\x85\xa4\xe1\xb4\x98\xe1\xb4\x8f\xe1\xb4\xa1\xe1\xb4\x87\xca\x80\xe2\x9a\xa1\xf0\x01\x01\xf8\x01A\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x01\xe0\x02\xf3\x94\xf6\xb1\x03'
        yout7 = b"\x06\x00\x00\x00\x8e\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*\x81\x01\x08\xb0\xa4\xdb\x80\x01\x1a'[f50057]\xd9\x85\xd9\x83\xd8\xa7\xd9\x81\xd8\xad\xd8\xa9.\xe2\x84\x93\xca\x99\xe3\x80\xb5..[f50057]2\x02ME@T\xb0\x01\x13\xb8\x01\xfc$\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xc1\xdb\x8d\xae\x03\xea\x01\x1d\xef\xbc\xad\xef\xbc\xa1\xef\xbc\xa6\xef\xbc\xa9\xef\xbc\xa1\xe3\x85\xa4\xe2\x8e\xb0\xe2\x84\x93\xca\x99\xe2\x8e\xb1\xf0\x01\x01\xf8\x01\xdb\x02\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x0f\xd8\x02>"
        yout8 = b'\x06\x00\x00\x00y\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*m\x08\xfd\x8a\xde\xb4\x02\x1a\x1f[f50057]ITZ\xe4\xb8\xb6MOHA\xe3\x85\xa42M[f50057]2\x02ME@C\xb0\x01\n\xb8\x01\xdf\x0f\xd8\x01\xac\xd8\xd0\xad\x03\xe0\x01\xf2\xdc\x8d\xae\x03\xea\x01\x15\xe3\x80\x9dITZ\xe3\x80\x9e\xe1\xb5\x97\xe1\xb5\x89\xe1\xb5\x83\xe1\xb5\x90\xf8\x01\x02\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x0e\xd8\x026'
        yout9 = b'\x06\x00\x00\x00w\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*k\x08\xc6\x99\xddp\x1a\x1b[f50057]HEROSHIIMA1[f50057]2\x02ME@I\xb0\x01\x01\xb8\x01\xe8\x07\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x1e\xef\xbc\xa8\xef\xbc\xa5\xef\xbc\xb2\xef\xbc\xaf\xef\xbc\xb3\xef\xbc\xa8\xef\xbc\xa9\xef\xbc\xad\xef\xbc\xa1\xef\xa3\xbf\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x01'
        yout10 = b'\x06\x00\x00\x00p\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*d\x08\xde\x91\xb7Q\x1a\x1c[f50057]SH\xe3\x85\xa4SHIMA|M[f50057]2\x02ME@R\xb0\x01\x14\xb8\x01\xe7C\xd8\x01\xdd\xd6\xd0\xad\x03\xe0\x01\xca\xdb\x8d\xae\x03\xea\x01\tSH\xe3\x85\xa4Team\xf8\x014\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x11\xd8\x02G\xe0\x02\x89\xa0\xf8\xb1\x03'
        yout11 = b'\x06\x00\x00\x00h\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*\\\x08\xa1\x9f\xb3\xf4\x01\x1a\x1b[f50057]2JZ\xe3\x85\xa4POWER[f50057]2\x02ME@M\xb0\x01\x13\xb8\x01\xa5(\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xec\xdb\x8d\xae\x03\xf0\x01\x01\xf8\x01\x9a\x01\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x0c\xd8\x02.\xe0\x02\xb2\xe9\xf7\xb1\x03'
        yout12 = b'\x06\x00\x00\x00\x8f\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*\x82\x01\x08\xaa\xe5\xa4\xe3\x01\x1a-[f50057]\xe3\x85\xa4\xd8\xb4\xd9\x83\xd8\xa7\xd9\x8e\xd9\x83\xd9\x80\xd9\x8a\xe3\x80\x8e\xe2\x85\xb5\xe1\xb4\x98\xe3\x80\x8f[f50057]2\x02ME@Q\xb0\x01\x13\xb8\x01\xf2*\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xaf\xdb\x8d\xae\x03\xea\x01\x15\xe2\x80\xa2\xe3\x85\xa4\xe2\x93\x8b\xe2\x92\xbe\xe2\x93\x85\xe3\x85\xa4\xe2\x80\xa2\xf8\x01q\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x13\xd8\x02e\xe0\x02\xa0\xf1\xf7\xb1\x03'
        yout13 = b'\x06\x00\x00\x00`\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*T\x08\xd2\xbc\xae\x07\x1a%[f50057]SYBLUS\xe3\x85\xa4\xe4\xba\x97\xe3\x85\xa4\xe3\x85\xa4\xe3\x85\xa4[f50057]2\x02ME@E\xb0\x01\x01\xb8\x01\xe8\x07\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x01'
        yout14 = b'\x06\x00\x00\x00\x86\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*z\x08\xfd\x8b\xf4\xfa\x01\x1a$[f50057]"\xd8\xaf\xd8\xb1\xd8\xa7\xd8\xba\xd9\x88\xd9\x86\xd9\x80\xd9\x88\xd9\x81"[f50057]2\x02ME@F\xb0\x01\x13\xb8\x01\xec \xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x12\xe1\xb4\x98\xe1\xb4\x84\xe1\xb5\x80\xe1\xb5\x89\xe1\xb5\x83\xe1\xb5\x90\xf0\x01\x01\xf8\x01\xb0\x02\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x04\xd8\x02\t\xe0\x02\xf2\x94\xf6\xb1\x03'
        yout15 = b'\x06\x00\x00\x00\x7f\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*s\x08\x90\xf6\x87\x15\x1a"[f50057]V4\xe3\x85\xa4RIO\xe3\x85\xa46%\xe3\x85\xa4zt[f50057]2\x02ME@M\xb0\x01\x13\xb8\x01\x95&\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb1\xdd\x8d\xae\x03\xea\x01\x0e\xe1\xb4\xa0\xe1\xb4\x80\xe1\xb4\x8d\xe1\xb4\x8f\xd1\x95\xf0\x01\x01\xf8\x01\xe2\x02\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x13\xd8\x02^\xe0\x02\x85\xff\xf5\xb1\x03'
        yout16 = b'\x06\x00\x00\x00s\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*g\x08\xaa\x84\xc1r\x1a\x1f[f50057]SA777RAWI\xe3\x85\xa4\xe3\x85\xa4[f50057]2\x02ME@N\xb0\x01\x13\xb8\x01\xc8\x1b\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x0cSA7RAWI\xe3\x85\xa4TM\xf0\x01\x01\xf8\x01\xfe\x01\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\t\xd8\x02 '
        yout17 = b'\x06\x00\x00\x00y\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*m\x08\xe7\xbf\xb6\x8f\x01\x1a\x1c[f50057]SVG.NINJA\xe2\xbc\xbd[f50057]2\x02ME@I\xb0\x01\x13\xb8\x01\x94\x1b\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\x85\xdb\x8d\xae\x03\xea\x01\x15\xe3\x85\xa4\xe3\x85\xa4\xe3\x85\xa4\xe3\x85\xa4???\xe3\x85\xa4\xe3\x85\xa4\xf0\x01\x01\xf8\x01o\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x10\xd8\x02?'
        yout18 = b"\x06\x00\x00\x00\x9d\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*\x90\x01\x08\xa8\xe8\x91\xd7\x01\x1a.[f50057]\xef\xbc\xa1\xef\xbc\xac\xef\xbc\x93\xef\xbc\xab\xef\xbc\xa5\xef\xbc\xa4\xe4\xba\x97\xef\xbc\xb9\xef\xbc\xb4\xe3\x85\xa4[f50057]2\x02ME@N\xb0\x01\x13\xb8\x01\x97'\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x1e\xef\xbc\xa1\xef\xbc\xac\xef\xbc\x93\xef\xbc\xab\xef\xbc\xa5\xef\xbc\xa4\xe2\x80\xa2\xef\xbc\xb9\xef\xbc\xb4\xe2\x9c\x93\xf0\x01\x01\xf8\x01\xab\x02\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x10\xd8\x02@\xe0\x02\xe9\x80\xf8\xb1\x03"
        yout19 = b'\x06\x00\x00\x00r\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*f\x08\x9b\x94\xaa\r\x1a\x1c[f50057]FARAMAWY_1M.[f50057]2\x02ME@I\xb0\x01\x01\xb8\x01\xe8\x07\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x12\xe2\x80\xa2\xe3\x85\xa4STRONG\xe3\x85\xa4\xe2\x80\xa2\xf0\x01\x01\xf8\x01X\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x01'
        yout20 = b'\x06\x00\x00\x00p\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*d\x08\xde\x91\xb7Q\x1a\x1c[f50057]SH\xe3\x85\xa4SHIMA|M[f50057]2\x02ME@R\xb0\x01\x14\xb8\x01\xe7C\xd8\x01\xdd\xd6\xd0\xad\x03\xe0\x01\xca\xdb\x8d\xae\x03\xea\x01\tSH\xe3\x85\xa4Team\xf8\x014\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x11\xd8\x02G\xe0\x02\x89\xa0\xf8\xb1\x03'
        yout21= b'\x06\x00\x00\x00h\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*\\\x08\xa1\x9f\xb3\xf4\x01\x1a\x1b[f50057]2JZ\xe3\x85\xa4POWER[f50057]2\x02ME@M\xb0\x01\x13\xb8\x01\xa5(\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xec\xdb\x8d\xae\x03\xf0\x01\x01\xf8\x01\x9a\x01\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x0c\xd8\x02.\xe0\x02\xb2\xe9\xf7\xb1\x03'
        yout22 = b'\x06\x00\x00\x00\x8f\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*\x82\x01\x08\xaa\xe5\xa4\xe3\x01\x1a-[f50057]\xe3\x85\xa4\xd8\xb4\xd9\x83\xd8\xa7\xd9\x8e\xd9\x83\xd9\x80\xd9\x8a\xe3\x80\x8e\xe2\x85\xb5\xe1\xb4\x98\xe3\x80\x8f[f50057]2\x02ME@Q\xb0\x01\x13\xb8\x01\xf2*\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xaf\xdb\x8d\xae\x03\xea\x01\x15\xe2\x80\xa2\xe3\x85\xa4\xe2\x93\x8b\xe2\x92\xbe\xe2\x93\x85\xe3\x85\xa4\xe2\x80\xa2\xf8\x01q\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x13\xd8\x02e\xe0\x02\xa0\xf1\xf7\xb1\x03'
        yout23 = b'\x06\x00\x00\x00\x86\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*z\x08\xfd\x8b\xf4\xfa\x01\x1a$[f50057]"\xd8\xaf\xd8\xb1\xd8\xa7\xd8\xba\xd9\x88\xd9\x86\xd9\x80\xd9\x88\xd9\x81"[f50057]2\x02ME@F\xb0\x01\x13\xb8\x01\xec \xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x12\xe1\xb4\x98\xe1\xb4\x84\xe1\xb5\x80\xe1\xb5\x89\xe1\xb5\x83\xe1\xb5\x90\xf0\x01\x01\xf8\x01\xb0\x02\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x04\xd8\x02\t\xe0\x02\xf2\x94\xf6\xb1\x03'
        yout24 = b'\x06\x00\x00\x00s\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*g\x08\xaa\x84\xc1r\x1a\x1f[f50057]SA777RAWI\xe3\x85\xa4\xe3\x85\xa4[f50057]2\x02ME@N\xb0\x01\x13\xb8\x01\xc8\x1b\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x0cSA7RAWI\xe3\x85\xa4TM\xf0\x01\x01\xf8\x01\xfe\x01\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\t\xd8\x02 '
        yout25 = b'\x06\x00\x00\x00y\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*m\x08\xe7\xbf\xb6\x8f\x01\x1a\x1c[f50057]SVG.NINJA\xe2\xbc\xbd[f50057]2\x02ME@I\xb0\x01\x13\xb8\x01\x94\x1b\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\x85\xdb\x8d\xae\x03\xea\x01\x15\xe3\x85\xa4\xe3\x85\xa4\xe3\x85\xa4\xe3\x85\xa4???\xe3\x85\xa4\xe3\x85\xa4\xf0\x01\x01\xf8\x01o\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x10\xd8\x02?'
        yout26 = b"\x06\x00\x00\x00\x9d\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*\x90\x01\x08\xa8\xe8\x91\xd7\x01\x1a.[f50057]\xef\xbc\xa1\xef\xbc\xac\xef\xbc\x93\xef\xbc\xab\xef\xbc\xa5\xef\xbc\xa4\xe4\xba\x97\xef\xbc\xb9\xef\xbc\xb4\xe3\x85\xa4[f50057]2\x02ME@N\xb0\x01\x13\xb8\x01\x97'\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x1e\xef\xbc\xa1\xef\xbc\xac\xef\xbc\x93\xef\xbc\xab\xef\xbc\xa5\xef\xbc\xa4\xe2\x80\xa2\xef\xbc\xb9\xef\xbc\xb4\xe2\x9c\x93\xf0\x01\x01\xf8\x01\xab\x02\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x10\xd8\x02@\xe0\x02\xe9\x80\xf8\xb1\x03"
        yout27 = b'\x06\x00\x00\x00r\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*f\x08\x9b\x94\xaa\r\x1a\x1c[f50057]FARAMAWY_1M.[f50057]2\x02ME@I\xb0\x01\x01\xb8\x01\xe8\x07\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x12\xe2\x80\xa2\xe3\x85\xa4STRONG\xe3\x85\xa4\xe2\x80\xa2\xf0\x01\x01\xf8\x01X\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x01'
        yout28 = b"\x06\x00\x00\x00\x82\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*v\x08\xaa\xdd\xf1'\x1a\x1d[f50057]BM\xe3\x85\xa4ABDOU_YT[f50057]2\x02ME@G\xb0\x01\x13\xb8\x01\xd4$\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x1d\xe2\x80\xa2\xc9\xae\xe1\xb4\x87\xca\x9f\xca\x9f\xe1\xb4\x80\xca\x8d\xe1\xb4\x80\xd2\x93\xc9\xaa\xe1\xb4\x80\xc2\xb0\xf0\x01\x01\xf8\x01\x8e\x01\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x07\xd8\x02\x16"
        yout29 = b'\x06\x00\x00\x00r\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*f\x08\x9a\xd6\xdcL\x1a-[f50057]\xe1\xb4\x8d\xcd\xa1\xcd\x9co\xe3\x85\xa4\xef\xbc\xa8\xef\xbc\xa1\xef\xbc\xa6\xef\xbc\xa9\xef\xbc\xa4\xef\xbc\xa9[f50057]2\x02ME@H\xb0\x01\x01\xb8\x01\xe8\x07\xea\x01\x15\xe1\xb4\x8d\xcd\xa1\xcd\x9co\xc9\xb4\xef\xbd\x93\xe1\xb4\x9b\xe1\xb4\x87\xca\x80\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x01'
        yout30 = b'\x06\x00\x00\x00v\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*j\x08\xb6\x92\xa9\xc8\x01\x1a [f50057]\xef\xbc\xaa\xef\xbc\xad\xef\xbc\xb2\xe3\x85\xa4200K[f50057]2\x02ME@R\xb0\x01\x13\xb8\x01\xc3(\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\n3KASH-TEAM\xf8\x012\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x06\xd8\x02\x13\xe0\x02\x89\xa0\xf8\xb1\x03'
        yout31 = b"\x06\x00\x00\x00\x92\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*\x85\x01\x08\xa2\xd3\xf4\x81\x07\x1a'[f50057]\xd8\xb3\xd9\x80\xd9\x86\xd9\x80\xd8\xaf\xd8\xb1\xd9\x8a\xd9\x84\xd8\xa71M\xe3\x85\xa4[f50057]2\x02ME@K\xb0\x01\x13\xb8\x01\xc1 \xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x1a\xef\xbc\xad\xef\xbc\xa6\xef\xbc\x95\xef\xbc\xb2\xef\xbc\xa8\xe3\x85\xa4\xe1\xb4\xa0\xc9\xaa\xe1\xb4\x98\xf0\x01\x01\xf8\x01\x8c\x01\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x0e\xd8\x024\xe0\x02\x87\xff\xf5\xb1\x03"
        yout32 = b'\x06\x00\x00\x00|\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*p\x08\xe0\xe1\xdeu\x1a\x1a[f50057]P1\xe3\x85\xa4Fahad[f50057]2\x02ME@N\xb0\x01\x13\xb8\x01\xd0&\xd8\x01\xea\xd6\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x1a\xe3\x85\xa4\xef\xbc\xb0\xef\xbc\xa8\xef\xbc\xaf\xef\xbc\xa5\xef\xbc\xae\xef\xbc\xa9\xef\xbc\xb8\xc2\xb9\xf0\x01\x01\xf8\x01\x9e\x03\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x0b\xd8\x02*'
        yout33 = b'\x06\x00\x00\x00\x82\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*v\x08\xc5\xcf\x94\x8b\x02\x1a\x18[f50057]@EL9YSAR[f50057]2\x02ME@P\xb0\x01\x13\xb8\x01\x86+\xd8\x01\xa2\xd7\xd0\xad\x03\xe0\x01\x89\xae\x8f\xae\x03\xea\x01\x1d-\xc9\xaa\xe1\xb4\x8d\xe1\xb4\x8d\xe1\xb4\x8f\xca\x80\xe1\xb4\x9b\xe1\xb4\x80\xca\x9fs\xe2\xac\x86\xef\xb8\x8f\xf8\x01j\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x14\xd8\x02\xe2\x02\xe0\x02\x9f\xf1\xf7\xb1\x03'
        yout34 = b'\x06\x00\x00\x00x\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*l\x08\xa9\x81\xe6^\x1a\x1e[f50057]STRONG\xe3\x85\xa4CRONA[f50057]2\x02ME@J\xb0\x01\x13\xb8\x01\xd8$\xd8\x01\xd8\xd6\xd0\xad\x03\xe0\x01\x92\xdb\x8d\xae\x03\xea\x01\x12\xe2\x80\xa2\xe3\x85\xa4STRONG\xe3\x85\xa4\xe2\x80\xa2\xf0\x01\x01\xf8\x01q\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x14\xd8\x02\xbc\x01'
        yout35 = b'\x06\x00\x00\x00\x7f\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*s\x08\xeb\x8d\x97\xec\x01\x1a&[f50057]\xd8\xb9\xd9\x80\xd9\x85\xd9\x80\xd8\xaf\xd9\x86\xd9\x8a\xd9\x80\xd8\xaa\xd9\x80\xd9\x88[f50057]2\x02ME@F\xb0\x01\x13\xb8\x01\xd3\x1a\xd8\x01\xaf\xd7\xd0\xad\x03\xe0\x01\xf4\xdc\x8d\xae\x03\xea\x01\rOSIRIS\xe3\x85\xa4MASR\xf8\x01o\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x13\xd8\x02\\\xe0\x02\xf4\x94\xf6\xb1\x03'
        yout36 = b'\x06\x00\x00\x00\x7f\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*s\x08\xb4\xff\xa3\xef\x01\x1a\x1c[f50057]ZAIN_YT_500K[f50057]2\x02ME@K\xb0\x01\x13\xb8\x01\xa3#\xd8\x01\xa2\xd7\xd0\xad\x03\xe0\x01\xbb\xdb\x8d\xae\x03\xea\x01\x1b\xe1\xb6\xbb\xe1\xb5\x83\xe1\xb6\xa4\xe1\xb6\xb0\xe3\x85\xa4\xe1\xb5\x97\xe1\xb5\x89\xe1\xb5\x83\xe1\xb5\x90\xf0\x01\x01\xf8\x01\\\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x0b\xd8\x02('
        yout37 = b'\x06\x00\x00\x00\x8f\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*\x82\x01\x08\x86\xa7\x9e\xa7\x0b\x1a([f50057]\xe2\x80\x94\xcd\x9e\xcd\x9f\xcd\x9e\xe2\x98\x85\xef\xbc\xa2\xef\xbc\xac\xef\xbc\xb2\xef\xbc\xb8[f50057]2\x02ME@d\xb0\x01\x13\xb8\x01\xe3\x1c\xe0\x01\xf2\x83\x90\xae\x03\xea\x01!\xe3\x85\xa4\xef\xbc\xa2\xef\xbc\xac\xef\xbc\xb2\xef\xbc\xb8\xe3\x85\xa4\xef\xbc\xb4\xef\xbc\xa5\xef\xbc\xa1\xef\xbc\xad\xe3\x85\xa4\xf8\x01u\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x13\xd8\x02Y\xe0\x02\xc1\xb7\xf8\xb1\x03'
        yout38 = b'\x06\x00\x00\x00\x85\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*y\x08\xc3\xcf\xe5H\x1a([f50057]\xe3\x85\xa4BEE\xe2\x9c\xbfSTO\xe3\x85\xa4\xe1\xb5\x80\xe1\xb4\xb5\xe1\xb4\xb7[f50057]2\x02ME@Q\xb0\x01\x14\xb8\x01\xffP\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xc1\xdb\x8d\xae\x03\xea\x01\x15TIK\xe2\x9c\xbfTOK\xe1\xb5\x80\xe1\xb4\xb1\xe1\xb4\xac\xe1\xb4\xb9\xf0\x01\x01\xf8\x01\xc8\x02\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x13\xd8\x02q'
        yout39 = b'\x06\x00\x00\x00\x94\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*\x87\x01\x08\x97\xd5\x9a.\x1a%[f50057]\xd8\xb9\xd9\x86\xd9\x83\xd9\x88\xd8\xb4\xe1\xb4\x80\xc9\xb4\xe1\xb4\x8b\xe3\x85\xa4[f50057]2\x02ME@P\xb0\x01\x13\xb8\x01\xe8(\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x1f\xe1\xb4\x80\xc9\xb4\xe1\xb4\x8b\xe1\xb4\x9c\xea\x9c\xb1\xca\x9c\xe3\x85\xa4\xe1\xb4\x9b\xe1\xb4\x87\xe1\xb4\x80\xe1\xb4\x8d\xf0\x01\x01\xf8\x01\xb6\x03\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\n\xd8\x02"\xe0\x02\xf2\x94\xf6\xb1\x03'
        yout40 = b'\x06\x00\x00\x00\x8a\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*~\x08\xf7\xdf\xda\\\x1a/[f50057]\xef\xbc\xa1\xef\xbc\xac\xef\xbc\xa8\xef\xbc\xaf\xef\xbc\xad\xef\xbc\xb3\xef\xbc\xa9_\xef\xbc\xb9\xef\xbc\xb4\xe2\x9c\x93[f50057]2\x02ME@P\xb0\x01\x13\xb8\x01\xb9*\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xc1\xdb\x8d\xae\x03\xea\x01\x0cALHOMSI~TEAM\xf0\x01\x01\xf8\x01\x8e\x0e\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x13\xd8\x02S\xe0\x02\xc3\xb7\xf8\xb1\x03'
        yout41 = b'\x06\x00\x00\x00\x86\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*z\x08\xb5\xdd\xec\x8e\x01\x1a%[f50057]\xd8\xa7\xd9\x88\xd9\x81\xe3\x80\x80\xd9\x85\xd9\x86\xd9\x83\xe3\x85\xa4\xe2\x9c\x93[f50057]2\x02ME@K\xb0\x01\x13\xb8\x01\xdd#\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x18\xef\xbc\xaf\xef\xbc\xa6\xe3\x85\xa4\xef\xbc\xb4\xef\xbc\xa5\xef\xbc\xa1\xef\xbc\xad\xe3\x85\xa4\xf0\x01\x01\xf8\x01\xe8\x02\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x13\xd8\x02Q'
        yout42 = b'\x06\x00\x00\x00\x8b\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*\x7f\x08\x81\xf4\xba\xf8\x01\x1a%[f50057]\xef\xbc\xa7\xef\xbc\xa2\xe3\x85\xa4\xef\xbc\xae\xef\xbc\xaf\xef\xbc\x91\xe3\x81\x95[f50057]2\x02ME@N\xb0\x01\x0c\xb8\x01\xbd\x11\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb1\xdd\x8d\xae\x03\xea\x01\x1a\xef\xbc\xa7\xef\xbc\xb2\xef\xbc\xa5\xef\xbc\xa1\xef\xbc\xb4__\xef\xbc\xa2\xef\xbc\xaf\xef\xbc\xb9\xf8\x018\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x0c\xd8\x02-\xe0\x02\x85\xff\xf5\xb1\x03'
        yout43 = b'\x06\x00\x00\x00o\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*c\x08\xfb\x9d\xb9\xae\x06\x1a\x1c[f50057]BT\xe3\x85\xa4BadroTV[f50057]2\x02ME@@\xb0\x01\x13\xb8\x01\xe7\x1c\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\x91\xdb\x8d\xae\x03\xea\x01\nBadro_TV_F\xf0\x01\x01\xf8\x01\x91\x1a\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\n\xd8\x02!'
        yout44 = b"\x06\x00\x00\x00s\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*g\x08\xc4\xe5\xe1>\x1a'[f50057]\xd8\xb5\xd8\xa7\xd8\xa6\xd8\xaf~\xd8\xa7\xd9\x84\xd8\xba\xd9\x86\xd8\xa7\xd8\xa6\xd9\x85[f50057]2\x02ME@J\xb0\x01\x14\xb8\x01\xceP\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x03Z7F\xf0\x01\x01\xf8\x01\xd0\x19\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x14\xd8\x02\x9c\x01"
        yout45 = b'\x06\x00\x00\x00\x85\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*y\x08\xfd\xa4\xa6i\x1a$[f50057]\xd8\xb2\xd9\x8a\xd9\x80\xd8\xb1\xc9\xb4\xcc\xb67\xcc\xb6\xca\x80\xe3\x85\xa4[f50057]2\x02ME@M\xb0\x01\x13\xb8\x01\xe1(\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x19\xc2\xb7\xe3\x85\xa4\xe3\x85\xa4N\xe3\x85\xa47\xe3\x85\xa4R\xe3\x85\xa4\xe3\x85\xa4\xc2\xb7\xf0\x01\x01\xf8\x01\x8f\t\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x13\xd8\x02k'
        yout46 = b'\x06\x00\x00\x00y\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*m\x08\xcc\xb9\xcc\xd4\x06\x1a"[f50057]\xd8\xa8\xd9\x88\xd8\xad\xd8\xa7\xd9\x83\xd9\x80\xd9\x80\xd9\x80\xd9\x85[f50057]2\x02ME@9\xb0\x01\x07\xb8\x01\xca\x0c\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x11*\xef\xbc\x97\xef\xbc\xaf\xef\xbc\xab\xef\xbc\xa1\xef\xbc\xad*\xf0\x01\x01\xf8\x01\xad\x05\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x01'
        yout47 = b'\x06\x00\x00\x00e\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*Y\x08\xe8\xbd\xc9b\x1a [f50057]\xe3\x80\x8cvip\xe3\x80\x8dDR999FF[f50057]2\x02ME@Q\xb0\x01\x10\xb8\x01\x94\x16\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xf0\x01\x01\xf8\x01\xa0\x04\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x0c\xd8\x02+'
        yout48 = b'\x06\x00\x00\x00\x82\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*v\x08\x86\xb7\x84\xf1\x01\x1a&[f50057]\xd8\xa2\xd9\x86\xd9\x8a\xd9\x80\xd9\x80\xd9\x84\xd8\xa7\xce\x92\xe2\x92\x91\xe3\x85\xa4[f50057]2\x02ME@Q\xb0\x01\x13\xb8\x01\x82)\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x13\xce\x92\xe2\x92\x91\xe3\x85\xa4MAFIA\xe3\x85\xa4\xef\xa3\xbf\xf0\x01\x01\xf8\x01\x95\x04\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x13\xd8\x02W'
        yout49 = b'\x06\x00\x00\x00u\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*i\x08\xb4\xbe\xde\x83\x02\x1a [f50057]SPONGEBOB!\xe3\x85\xa4\xe4\xba\x97[f50057]2\x02ME@N\xb0\x01\x14\xb8\x01\x842\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\x96\xdb\x8d\xae\x03\xea\x01\x0cALHOMSI~TEAM\xf0\x01\x01\xf8\x01\xbd\x03\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x13\xd8\x02{'
        yout50 = b'\x06\x00\x00\x00u\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*i\x08\xb4\xbe\xde\x83\x02\x1a [f50057]SPONGEBOB!\xe3\x85\xa4\xe4\xba\x97[f50057]2\x02ME@N\xb0\x01\x14\xb8\x01\x842\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\x96\xdb\x8d\xae\x03\xea\x01\x0cALHOMSI~TEAM\xf0\x01\x01\xf8\x01\xbd\x03\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x13\xd8\x02{'
        yout51 = b'\x06\x00\x00\x00v\x08\xd4\xd7\xfa\xba\x1d\x10\x06 \x02*j\x08\xb8\xa6\x85\xc5\x01\x1a\x1b[f50057]DARBKA\xe3\x85\xa41M[f50057]2\x02ME@Q\xb0\x01\x13\xb8\x01\x90(\xd8\x01\xd4\xd8\xd0\xad\x03\xe0\x01\xb2\xdd\x8d\xae\x03\xea\x01\x12LAST\xe2\x80\x8f\xe3\x85\xa4POWER\xe2\x9a\xa1\xf0\x01\x01\xf8\x01\x92\x03\x80\x02\xfd\x98\xa8\xdd\x03\x90\x02\x01\xd0\x02\x13\xd8\x02W'
        yout_list = [yout1,yout2,yout3,yout4,yout5,yout6,yout7,yout8,yout9,yout10,yout11,yout12,yout13,yout14,yout15,yout16,yout17,yout18,yout19,yout20,yout21,yout22,yout23,yout24,yout25,yout26,yout27,yout28,yout29,yout30,yout31,yout32,yout33,yout34,yout35,yout36,yout37,yout38,yout39,yout40,yout41,yout42,yout43,yout44,yout45,yout46,yout47,yout48,yout49,yout50,yout51]

        global cmodeinfo
        cmodeinfo = True

        global cmodeloop
        cmodeloop = False

        global full


        global exitpacket
        global enterpacket
        exitpacket = b''
        enterpacket = b''
        idinfo = True
        global visible_ret
        global fivesq
        kema = False
        activation = True
        global roba
        packet0300 = True
        roba = 1
        stat = True
        global startspammsg
        startspammsg = False

        global lg_room
        lg_room = False

        global fivesq
        fivesq = False


        global inv_ret
        inv_ret = False



        
        ########

        while True:
            ######################################
            #spam messages

            global spamsg
            def spamsg(value):
                global startspammsg
                startspammsg = value
                return startspammsg


            # crazymode

            



            ######################################
            r, w, e = select.select([client, remote], [], [])
            global start
            global full
            global hidd
            if client in r or remote in r:
                global serversocket
                global remotesockett
                global clientsockett
                if client in r:
                    global team
                    global one
                    global teams
                    global packett1
                    global levelplus
                    global packett
                    global vispacket
                    global dataC
                    global five
                    global lag_status
                    global cw
                    
                    dataC = client.recv(999999)

                    global hide
                    hide =False
                    global recordmode

                    if '0515' in dataC.hex()[0:4] and len(dataC.hex()) >= 141:
                        hide = True
                    if '0515' in dataC.hex()[0:4] and 700 < len(dataC.hex()) < 1100:   #ENTER TO SQUAD
                       team = remote
                       teams = client
                       packett = dataC
                       print("ENTER TO SQUAD Def")

                    if '0515' in dataC.hex()[0:4] and 30 < len(dataC.hex()) < 50:   #EXIT FROM SQUAD
                       packett1 = dataC
                       print("EXIT FROM SQUAD Def")

                    if recordmode ==True:
                        if '1215' in dataC.hex()[0:4]:
                            global spampacket
                            spampacket = dataC
                            recordmode = False
                            global statues
                            statues= True
                            # print('closeing record ')
                            b = threading.Thread(target=spam, args=(remote,spampacket))
                            b.start()
                    #####


                    if port == 39699:
                        five = remote
                        cw = client


                    if remote.send(dataC) <= 0:
                            break
                if remote in r:

                    ######
                    global defult_value
                    global invvs
                    global invvspacket
                    
                    global hidr
                    global cliee
                    global lag
                    global newdataS
                    global newdataSofspam
                    global newdataSoffspam
                    global clieee
                    global backto
                    global actcode
                    global returntoroom
                    global newbackdataS
                    global getin
                    global spaminv
                    global spammsg
                    global preventlag
                    global sqlag
                    global ingroup5
                    global group5
                    global invite
                    global roomp
                    global number
                    global acctive
                    global invtoroom
                    global msgact
                    global lagscript
                    global lagmsg
                    global stoplag
                    global command
                    global stopmsg
                    ######
                    global full
                    #####


                    #####



                    global listt
                    global C
                    global istarted
                    global gameplayed
                    global packet
                    global socktion
                    global increase
                    global roomp
                    global roomretst
                    global number
                    global invtoroom
                    global invtoroompacket
                    global snv
                    global add_yout
                    global newdataS2
                    global msggg1
                    global msggg2
                    global enc_client_id
                    global packet1
                    global dataS

                    dataS = remote.recv(999999)


                    if b"/help" in dataS and command == True:
                        print("Done Help")
                        client.send(bytes.fromhex(gen_msgv2_clan(f"[bِ][cِ][f50057]أوامـر تـشـغـيـل الـبـوت !",dataS.hex())))
                        client.send(bytes.fromhex(gen_msgv2_clan(f"[bِ][cِ]--------------------------------",dataS.hex())))
                        client.send(bytes.fromhex(gen_msgv2_clan(f"[bِ][cِ][00FِF00] تدمير فريقㅤ\n\n-ِِ-ِid\n\n[ff00ff]لازم تكون صولو",dataS.hex())))
                        client.send(bytes.fromhex(gen_msgv2_clan(f"[bِ][cِ][00FِF00] دخـول سكواد غير مرئي\n\n-ِ+id",dataS.hex())))
                        client.send(bytes.fromhex(gen_msgv2_clan(f"[bِ][cِ][00FِF00] دخـول سكواد ظـاهر\n\n+ِ+ِid",dataS.hex())))
                        client.send(bytes.fromhex(gen_msgv2_clan(f"[bِ][cِ][00FِF00]جلب معلومات عن لاعب\n\n/ِ+id",dataS.hex())))
                        client.send(bytes.fromhex(gen_msgv2_clan(f"[bِ][cِ][00FِF00]رجوع للروم لو حد طردك\n\n/rِet",dataS.hex())))
                        client.send(bytes.fromhex(gen_msgv2_clan(f"[bِ][cِ][00FِF00]رجوع للروم مخفي لما تنطرد\n\n/rِef",dataS.hex())))
                        client.send(bytes.fromhex(gen_msgv2_clan(f"[bِ][cِ][00FِF00]دخول أي روم مخـفي\n\n/rِid\n\nid الروم",dataS.hex())))
                        client.send(bytes.fromhex(gen_msgv2_clan(f"[bِ][cِ][00FِF00]صـديـق وهـمي\n\n/fِid\n\nid الشخص",dataS.hex())))
                        client.send(bytes.fromhex(gen_msgv2_clan(f"[bِ][cِ] إضافة جميع اليوتيوبرز",dataS.hex())))
                        client.send(bytes.fromhex(gen_msgv2_clan(f"[bِ][cِ] الوضـع الـمـجـنـون [00ِff00]",dataS.hex())))
                        client.send(bytes.fromhex(gen_msgv2_clan(f"[bِ][cِ] 5 في المجموعة [ff000ِ0]\n\n/55ِ5",dataS.hex())))
                        client.send(bytes.fromhex(gen_msgv2_clan(f"[bِ][cِ] رجوع مخفي للسكواد",dataS.hex())))
                        client.send(bytes.fromhex(gen_msgv2_clan(f"[bِ][cِ]سـبـام طـلـبـات إنضـمـام",dataS.hex())))
                        client.send(bytes.fromhex(gen_msgv2_clan(f"[bِ][cِ] سبام رسائل ",dataS.hex())))
                        client.send(bytes.fromhex(gen_msgv2_clan(f"[bِ][cِ]بدء إجباري [ff000ِ0]\n\n/sِss",dataS.hex())))
                    else:
                        if client.send(dataS) <= 0:
                            break

                        if '1200' in dataS.hex()[:4] and one == True :
                            
                            one = False
                            start_marker = "08"
                            end_marker = "10"
                            msggg1 = client
                            msggg2 = remote

                            start_index = dataS.hex().find(start_marker) + len(start_marker)
                            end_index = dataS.hex().find(end_marker, start_index)

                            if start_index != -1 and end_index != -1:
                                enc_client_id = dataS.hex()[start_index:end_index]
                                print(f"Encrypted Player id : {enc_client_id}")

                        if '1200' in dataS.hex()[0:4] and b'--' in dataS and 700 > len(dataS.hex()) and command == True:
                            print("destroy!")
                            if b"***" in dataS:
                                dataS = dataS.replace(b"***",b"106")
                            newdataS2 = dataS.hex()
                            lag_status = True
                            text = str(bytes.fromhex(newdataS2))
                            match = re.search(r'\-\-(.*?)\(', text)
                            numb = match.group(1)
                            if int(numb) / int(numb) == 1 and len(numb) < 11:
                                target_id = convert_id(str(numb))
                                threading.Thread(target=start_des,args=(target_id,five)).start()


                        if '1200' in dataS.hex()[0:4] and b'++' in dataS and "1215" and command == True:
                            if b"***" in dataS:
                                    dataS = dataS.replace(b"***",b"106")
                            newdataS2 = dataS.hex()
                            text = str(bytes.fromhex(newdataS2))
                            match = re.search(r'\+\+(.*?)\(', text)
                            number = match .group(1)
                            if int(number) / int(number) == 1 and len(number) < 11:
                                target_id = convert_id(str(number))
                                threading.Thread(target=visible_ent,args=(target_id,)).start()


                        if b"/555" in dataS and "1215" in dataC.hex()[0:4] and command == True:
                            threading.Thread(target=g5,args=(enc_client_id,cw,five,client,dataS.hex())).start()



                        if '1200' in dataS.hex()[0:4] and b'-+' in dataS and command == True:
                                    if b"***" in dataS:
                                        dataS = dataS.replace(b"***",b"106")
                                    print("enteeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeeer")
                                    newdataS2 = dataS.hex()
                                    text = str(bytes.fromhex(newdataS2))
                                    match = re.search(r'\-\+(.*?)\(', text)
                                    number = match .group(1)
                                    if int(number) / int(number) == 1 and len(number) < 11:
                                        target_id = convert_id(str(number))
                                        threading.Thread(target=inv_ent,args=(target_id,)).start()



                        if "1200" in dataS.hex()[0:4] and b"/r" in dataS and 700 > len(dataS.hex()) and command == True:
                            if b"***" in dataS:
                                dataS = dataS.replace(b"***",b"106")
                            start_marker = b'/r'
                            end_marker = b'('
                            start_index = dataS.find(start_marker) + len(start_marker)
                            end_index = dataS.find(end_marker, start_index)
                            value_bytes = dataS[start_index:end_index]
                            value = value_bytes.decode('utf-8')
                            print(value)
                            if len(value) < 9 and int(value)/int(value) == 1:
                                print(value)
                                room_id = convert_id(value)                 
                                cw.send(bytes.fromhex(f"0e0000029208{enc_client_id}100e20052a85050aae0108{enc_client_id}10{enc_client_id}1a0f42595445e385a4424f54e385a45633206430014a0f010407090a0b120d0f16191a1e20235801600168e8077001800181d08d81b9f58cbd17b201600a5a68747470733a2f2f6c68332e676f6f676c6575736572636f6e74656e742e636f6d2f612f414163485474644e756868595a377936422d5a45726b77536d686758383651626b4170316f53414b31384e376c5836423d7339362d6310011801ba0102080112d10308{room_id}12134d4f48414d4544e385a44259544520d8bad8b118d3b1b0b91c2001280f3802401e52033535355ab70108{enc_client_id}1aae0108{enc_client_id}10{enc_client_id}1a0f42595445e385a4424f54e385a45633206430014a0f010407090a0b120d0f16191a1e20235801600168e8077001800181d08d81b9f58cbd17b201600a5a68747470733a2f2f6c68332e676f6f676c6575736572636f6e74656e742e636f6d2f612f414163485474644e756868595a377936422d5a45726b77536d686758383651626b4170316f53414b31384e376c5836423d7339362d6310011801ba010208015abc0108d3b1b0b91c1ab30108d3b1b0b91c10d3b1b0b91c1a0e4d4f48414d4544e385a442595445206428a7f48fae0330014a0f010407090a0b120d0f16191a1e202358016001688b0870037806800182d08d81b9f58cbd17b201600a5a68747470733a2f2f6c68332e676f6f676c6575736572636f6e74656e742e636f6d2f612f4141634854746372366e6753636c6d446839554d4c7878374c67725a387235555333594258357936316a4437686c4e5a3d7339362d6310011801ba01006801700178019001c092d1519801c8c89005da0100e80101f00101f80180d08d81b9f58cbd178202020101"))


                        if cmode == True and cmodeinfo==True:
                            cmodeloop = True
                            cmodeinfo = False
                            threading.Thread(target=crazymode,args=(team,packett1,packett)).start()

                        if cmode == False:
                            cmodeloop = False
                            cmodeinfo = True



                        if '1200' in dataS.hex()[0:4] and b'GroupID' in dataS and packet0300 == True  :
                                from time import sleep
                                lis = [p1,p2,p3,p4,p5,xmoodz]
                                for msg in lis:
                                    remote.send(msg)
                                    sleep(0.3)
                                packet0300 = False

                        if b"/sss" in dataS and "1215" in dataC.hex()[0:4] and command == True:
                            print("Start_game")
                            threading.Thread(target=enter_to_game,args=(enc_client_id,)).start()
                            



                        if  port == 39699:
                            invite = client
                            snv = remote


                        if startspammsg == True:     #/spam
                           recordmode = True



                        if startspammsg == False: #/f
                            statues = False

                        if '0e00' in dataS.hex()[0:4]:
                           for i in range(10):
                               pattern = fr"x0{str(i)}(\d+)Z"
                               match = re.search(pattern, str(dataS))
                               if match:
                                   number = match.group(1)
                                   roomp = True
                                   if number != defult_value:
                                        print("Done Catch packet")
                                        invvs = client
                                        invvspacket = dataS
                                        defult_value = number

                                   break
                           if match:
                               pass
                           else:
                               if "OPENATTRIBUTESEXT" in str(dataS):
                                    pass

                        if  '0500' in dataS.hex()[0:4] and hide == True :
                            if len(dataS.hex())<=30:
                                hide = True
                            if len(dataS.hex())>=100:
                                packet1 = dataS
                                hidd = client
                                hide = False

                        if b"/ref" in dataS and "1200" in dataS.hex()[0:4] and 430 > len(dataS.hex()) > 200 and command == True:

                                print("Done Send Packet ..")
                                invvs.send(invvspacket)


                        if b"/rec" in dataS and '1200' in dataS.hex()[0:4]:
                            remote.send(b'\x05\x03\x00\x00')

                        if b"/startt" in dataS:
                            command = True

                        if '1200' in dataS.hex()[0:4] and b'/f' in dataS and command == True:
                                if b"***" in dataS:
                                    dataS = dataS.replace(b"***",b"106")
                                start_marker = b'/f'
                                end_marker = b'('
                                start_index = dataS.find(start_marker) + len(start_marker)
                                end_index = dataS.find(end_marker, start_index)
                                value_bytes = dataS[start_index:end_index]
                                number = value_bytes.decode('utf-8')
                                if int(number) / int(number) == 1 and len(number) < 11:
                                    target_id = convert_id(str(number))
                                    threading.Thread(target=fake_frind,args=(target_id,cw)).start()



                        if '1200' in dataS.hex()[0:4] and b'/+' in dataS  and idinfo == True and command == True:
                                start_marker = b'/+'
                                end_marker = b'('
                                start_index = dataS.find(start_marker) + len(start_marker)
                                end_index = dataS.find(end_marker, start_index)
                                value_bytes = dataS[start_index:end_index]
                                number = value_bytes.decode('utf-8')
                                if int(number) / int(number) == 1 and len(number) < 11:
                                    newdataS2 = dataS.hex()
                                    getin = client          
                                    threading.Thread(target=player_info,args=(number,getin,newdataS2)).start()

                        if add_yout == True:
                            add_yout = False
                            from time import sleep
                            for h in yout_list:
                                    invite.send(h)
                                    sleep(0.2)

                        if b'/ret' in dataS and '1200' in dataS.hex()[0:4] and 700 > dataS.hex():
                               clieee.send(lag)
                           
                        

def startt():
    try:
        threading.Thread(target=sayhello).start()
        Proxy().runs('127.0.0.1',1080)
    except Exception as e:
            print(e)
