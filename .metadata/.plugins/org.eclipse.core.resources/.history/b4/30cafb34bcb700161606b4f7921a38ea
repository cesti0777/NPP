
import java.io.*;
import java.net.*;
import java.util.*;

public class Client {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		Socket sock=null;
		ObjectInputStream ois = null;
		ObjectOutputStream oos =null;
		boolean endFlag = false;
		String id = "seong";
		CodeReviewFrame frame;
		
		try{
			sock = new Socket("127.0.0.1",11002);
			System.out.println("접속에 성공했습니다.");
			
			oos = new ObjectOutputStream(sock.getOutputStream());
			ois = new ObjectInputStream(sock.getInputStream());
			frame = new CodeReviewFrame(oos);
			
			//접속자 id를 알려 주는 패킷
			Packet packet = new Packet();
			packet.setMsgType(3);
			packet.setId(id);	
			oos.writeObject(packet);
			oos.flush();
			
			System.out.println("메세지 보내기 성공");
			
			InputThread it = new InputThread(sock, ois, frame);
			it.start();
			
		}
		catch(Exception e){
			System.out.println(e);
			
		}
	}
}

class InputThread extends Thread{
	private Socket sock;
	private ObjectInputStream ois;
	private CodeReviewFrame crf;
	
	InputThread(Socket sock, ObjectInputStream ois, CodeReviewFrame crf){
		this.sock = sock;
		this.ois = ois;
		this.crf = crf;
	}
	
	public void run(){
	
		Packet packet;
		String code;
		
		try {
			
			while((packet = (Packet)ois.readObject()) != null){
				switch(packet.getMsgType()){
				
				//에디터 타이핑 
				case 0:
					break;
					
				//채팅 
				case 1:
					break;
				
				//컴파일
				case 2:
					crf.setConsole(packet.getSourceCode());
					break;
				case 3 :
					crf.setPeople(packet.getId());
					break;
					
				}
			}
			
		} catch (Exception e) {
			System.out.println(e);
		}
		finally{
			
			try{
				if(ois != null){
					ois.close();
				}
			}
			catch(Exception e){
				
			}
			try{
				if(sock != null){
					sock.close();
				}
			}
			catch(Exception e){
				
			}			
		}
	}
}
