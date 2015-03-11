import java.util.Stack;

public class Expression {
	Stack<Type> types;
	Stack<Op> operations;
	
	public Expression() {
		this.types = new Stack<Type>();
		this.operations = new Stack<Op>();
	}

	void ajoutType(Type t){
		types.push(t);
	}
	
	void ajoutOp(Op op){
		operations.push(op);
	}
	
	Type testAddSubMulDiv(Type type1, Type type2){
		if(type1 == Type.INT){
			if(type2 == Type.INT){
				return Type.INT;
			}
		}
		return Type.ERROR;
	}
	
	Type testSupInf(Type type1, Type type2){
		if(type1 == Type.INT){
			if(type2 == Type.INT){
				return Type.BOOL;
			}
		}
		return Type.ERROR;
	}
	
	Type testEQU(Type type1, Type type2){
		if(type1 == Type.INT){
			if(type2 == Type.INT){
				return Type.BOOL;
			}
		}
		if(type1 == Type.BOOL){
			if(type2 == Type.BOOL){
				return Type.BOOL;
			}
		}
		return Type.ERROR;
	}
	
	Type testAndOr(Type type1, Type type2){
		if(type1 == Type.BOOL){
			if(type2 == Type.BOOL){
				return Type.BOOL;
			}
		}
		return Type.ERROR;
	}
	
	void testStacks(){
		while(operations.peek() != null){
			switch(operations.pop()){
			case PLUS :
				Yaka.yvm.iadd();
				ajoutType(testAddSubMulDiv(types.pop(), types.pop()));
				break;
			case MOINS :
				Yaka.yvm.isub();
				ajoutType(testAddSubMulDiv(types.pop(), types.pop()));
				break;
			case MUL :
				Yaka.yvm.imul();
				ajoutType(testAddSubMulDiv(types.pop(), types.pop()));
				break;
			case DIV :
				Yaka.yvm.idiv();
				ajoutType(testAddSubMulDiv(types.pop(), types.pop()));
				break;
			case INF :
				Yaka.yvm.iinf();
				ajoutType(testSupInf(types.pop(), types.pop()));
				break;
			case SUP :
				Yaka.yvm.isup();
				ajoutType(testSupInf(types.pop(), types.pop()));
				break;
			case INFE :
				Yaka.yvm.iinfegal();
				ajoutType(testSupInf(types.pop(), types.pop()));
				break;
			case SUPE :
				Yaka.yvm.isupegal();
				ajoutType(testSupInf(types.pop(), types.pop()));
				break;
			case EQU :
				Yaka.yvm.iegal();
				ajoutType(testEQU(types.pop(), types.pop()));
				break;
			case DIFF :
				Yaka.yvm.idiff();
				ajoutType(testEQU(types.pop(), types.pop()));
				break;
			case OR :
				Yaka.yvm.ior();
				ajoutType(testAndOr(types.pop(), types.pop()));
				break;
			case AND :
				Yaka.yvm.iand();
				ajoutType(testAndOr(types.pop(), types.pop()));
				break;
			default :
				ajoutType(Type.ERROR);
			}
		}
	}
	
	public void pushInteger(int a) {
		this.types.push(Type.INT);
		Yaka.yvm.iconst(a);
	}
		
	public void pushBoolean(int a) {
		this.types.push(Type.BOOL);
		Yaka.yvm.iconst(a);
	}
	
	public void pushIdent(String id) {
		Ident ident = Yaka.tabIdent.getIdent(id);
		if(ident!=null) {
			this.types.push(ident.getType());
			if(ident.isVar()) {
				Yaka.yvm.iload(((IdVar)ident).getOffset());
			} else if(ident.isConst()) {
				Yaka.yvm.iconst(((IdConst)ident).getValue());
			} else {
				//Erreur
			}
		} else {
			this.stackType.push(Type.ERROR);
			//Erreur
		}
	}

}
